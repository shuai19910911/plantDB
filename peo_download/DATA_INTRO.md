# Plant Gene Expression Omnibus 数据介绍与下载记录

更新时间：2026-06-03 08:30 CST

## 数据源

- 原始入口：[https://expression.plant.tools/](https://expression.plant.tools/)
- 实际站点：[https://peo.ku.dk/](https://peo.ku.dk/)
- 数据库名称：Plant Gene Expression Omnibus (PEO)
- 网站描述：跨植物器官的植物基因表达资源。
- 维护方页面标识：Mutwil Lab, NTU Singapore。

## 已确认的数据内容

PEO 是一个植物基因表达检索网站，首页显示覆盖 147 个植物物种。网站支持按基因 ID、蛋白序列相似性、PFAM 结构域、MapMan 功能分类、物种和器官浏览表达数据。

当前已下载并解析的第一阶段数据来自 `/species` 页面服务端渲染数据，包含 147 个物种的元信息：

- NCBI taxonomy id
- 物种学名
- 样本数 `n_samples`
- 已注释样本数 `n_annotated_samples`
- CDS 序列来源名称
- CDS 源 URL
- 数据库内部 `_id`
- 创建和更新时间字段

## 当前体量预估

第一阶段抓取了网站页面和物种元数据，体量较小：

- HTML/JS 页面快照：约 0.1 MB 级别
- 147 个物种元数据 JSON/TSV：< 1 MB

根据 Next.js 数据接口和 API 探测，PEO 本站可直接下载的数据至少包括：

- 147 个物种元数据
- 147 个物种的基因分页索引，每条基因记录包含基因 ID、内部 ID、注释 ID、邻居基因相关系数、MapMan/PFAM 注释摘要
- 器官本体或器官分类数据
- PFAM/InterPro 注释索引
- MapMan 功能分类索引
- 外部 CDS FASTA 来源 URL 清单；这些是引用的外部序列来源，不一定由 PEO 本站托管

当前已确认的完整物种基因分页规模：

- 物种：147
- 基因分页：126,786 页
- 分页大小：每页 50 个基因
- 全量基因分页 JSON 估算大小：约 36.25 GB
- 当前已下载的第一页/索引/元数据实际占用：约 46 MB

下一阶段会通过 Next.js 静态包和 `/api/...` 端点确认可直接下载的数据文件与总大小。

## 下载记录

### 阶段 1：站点入口与物种页快照

状态：已完成

本地位置：

- `peo_download/site/species.html`
- `peo_download/site/help.html`
- `peo_download/site/buildManifest.js`

说明：

- `https://expression.plant.tools/` 会重定向到 `https://peo.ku.dk/`。
- `/species` 页面确认包含完整 147 物种列表。
- `/help` 页面确认网站支持按基因 ID、蛋白序列、PFAM、MapMan、物种页面检索。

### 阶段 2：物种元数据结构化导出

状态：已完成

本地位置：

- `peo_download/metadata/species.json`
- `peo_download/metadata/species.tsv`
- `peo_download/metadata/cds_sources.tsv`
- `peo_download/metadata/species_summary.json`

统计结果：

- 物种数：147
- 总样本数：61,868
- 已注释样本数：43,541
- CDS 来源类别数：40
- CDS URL 类型：HTTP/HTTPS 79 个，FTP 58 个，空 URL 9 个，其他文本 1 个

说明：

- PEO 的物种表引用了大量外部 CDS FASTA/FASTA.gz 来源；这些 URL 是物种注释来源，不一定等同于 PEO 本站表达数据下载。
- 当前已保存的是 PEO 网站自身暴露的物种元数据，不会递归下载外部机构的大型 FASTA，除非后续确认这些属于用户希望的“所有数据”范围。

### 阶段 3：API 与静态资源发现

状态：已完成

本地位置：

- `peo_download/site/*.js`
- `peo_download/api/interpro/page_*.json`
- `peo_download/api/interpro.all.json`
- `peo_download/api/mapman/page_*.json`
- `peo_download/api/mapman.all.json`
- `peo_download/metadata/organs.json`
- `peo_download/api/species_pages.summary.json`
- `peo_download/logs/download_summary.json`

发现的主要接口/数据路径：

- `/_next/data/rnbMI0Jsua1h7MQJRLSqK/species/{taxid}.json?taxid={taxid}&pageIndex={n}&pageSize=50`
- `/api/interpro?pageIndex={n}&pageSize=1000`
- `/api/mapman?pageIndex={n}&pageSize=1000`
- `/organs` SSR 数据中的 `poTerms`

已完成下载：

- 器官/组织 PO 术语：109 条
- PFAM/InterPro 注释索引：8,704 条，9 个分页文件
- MapMan 注释索引：145 条，3 个分页文件
- 147 个物种的第一页基因分页，用于估算完整基因索引体量

说明：

- `/_next/data/.../species/{taxid}.json` 的分页参数有效；例如 `pageIndex=0` 与 `pageIndex=1` 返回不同的 50 条基因。
- 每条基因分页记录含 50 个邻居基因相关系数，因此全量体量明显大于只保存基因 ID。
- 目前尚未下载 126,786 个完整物种基因分页；这是下一阶段的大体量下载。

### 阶段 4：完整物种基因分页下载

状态：待开始

计划：

- 使用 `peo_download/download_peo_data.py` 断点续传下载全部物种分页。
- 预计新增下载量约 36.25 GB。
- 预计请求数约 126,786 次；脚本当前每页请求后短暂停顿，适合长时间运行。
- 已保存的每个物种第一页会被复用，不会重复下载。
- 2026-06-03 08:18:06 CST：阶段 4 开始：按物种分页下载完整基因索引。
- 2026-06-03 08:23:47 CST：阶段 4 开始：按物种分页下载完整基因索引。
- 2026-06-03 08:34:10 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655。
- 2026-06-03 08:36:37 CST：阶段 4 开始：按物种分页下载完整基因索引。
- 2026-06-03 08:36:41 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655。
- 2026-06-03 08:41:49 CST：阶段 4 开始：按物种分页下载完整基因索引。
- 2026-06-03 08:41:53 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655。
- 2026-06-03 08:47:18 CST：阶段 4 开始：按物种分页下载完整基因索引。
- 2026-06-03 08:47:22 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655, failed_pages=0。
- 2026-06-03 09:07:34 CST：阶段 4 物种完成 2/147：tax=4081, Solanum lycopersicum, pages=682, genes=34075, failed_pages=0。
- 2026-06-03 09:21:10 CST：阶段 4 物种完成 3/147：tax=29760, Vitis vinifera, pages=527, genes=26346, failed_pages=0。
- 2026-06-03 09:28:11 CST：阶段 4 物种完成 4/147：tax=3055, Chlamydomonas reinhardtii, pages=355, genes=17741, failed_pages=0。
- 2026-06-03 09:47:54 CST：阶段 4 物种完成 5/147：tax=3218, Physcomitrella patens, pages=650, genes=32458, failed_pages=0。


- 2026-06-03 09:55:55 CST：阶段 4 开始：按物种分页下载完整基因索引。

- 2026-06-03 09:56:00 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655, failed_pages=0。

- 2026-06-03 09:56:07 CST：阶段 4 物种完成 2/147：tax=4081, Solanum lycopersicum, pages=682, genes=34075, failed_pages=0。

- 2026-06-03 09:56:11 CST：阶段 4 物种完成 3/147：tax=29760, Vitis vinifera, pages=527, genes=26346, failed_pages=0。

- 2026-06-03 09:56:14 CST：阶段 4 物种完成 4/147：tax=3055, Chlamydomonas reinhardtii, pages=355, genes=17741, failed_pages=0。

- 2026-06-03 09:56:19 CST：阶段 4 物种完成 5/147：tax=3218, Physcomitrella patens, pages=650, genes=32458, failed_pages=0。

- 2026-06-03 11:31:15 CST：阶段 4 物种完成 6/147：tax=3329, Picea abies, pages=1333, genes=66632, failed_pages=3。

- 2026-06-03 11:39:38 CST：阶段 4 物种完成 7/147：tax=3197, Marchantia polymorpha, pages=389, genes=19421, failed_pages=16。

- 2026-06-03 11:53:44 CST：阶段 4 物种完成 8/147：tax=88036, Selaginella moellendorffii, pages=446, genes=22285, failed_pages=0。

- 2026-06-03 12:14:09 CST：阶段 4 物种完成 9/147：tax=13333, Amborella trichopoda, pages=547, genes=27313, failed_pages=0。

- 2026-06-03 12:34:15 CST：阶段 4 物种完成 10/147：tax=2762, Cyanophora paradoxa, pages=495, genes=24702, failed_pages=2。

- 2026-06-03 12:41:33 CST：阶段 4 开始：按物种分页下载完整基因索引。

- 2026-06-03 12:41:43 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655, failed_pages=0。

- 2026-06-03 12:41:53 CST：阶段 4 物种完成 2/147：tax=4081, Solanum lycopersicum, pages=682, genes=34075, failed_pages=0。

- 2026-06-03 12:42:02 CST：阶段 4 物种完成 3/147：tax=29760, Vitis vinifera, pages=527, genes=26346, failed_pages=0。

- 2026-06-03 12:42:08 CST：阶段 4 物种完成 4/147：tax=3055, Chlamydomonas reinhardtii, pages=355, genes=17741, failed_pages=0。

- 2026-06-03 12:42:19 CST：阶段 4 物种完成 5/147：tax=3218, Physcomitrella patens, pages=650, genes=32458, failed_pages=0。

- 2026-06-03 12:49:42 CST：阶段 4 物种完成 6/147：tax=3329, Picea abies, pages=1333, genes=66632, failed_pages=2。

- 2026-06-03 12:53:14 CST：阶段 4 物种完成 7/147：tax=3197, Marchantia polymorpha, pages=389, genes=19421, failed_pages=0。

- 2026-06-03 12:53:21 CST：阶段 4 物种完成 8/147：tax=88036, Selaginella moellendorffii, pages=446, genes=22285, failed_pages=0。

- 2026-06-03 12:53:30 CST：阶段 4 物种完成 9/147：tax=13333, Amborella trichopoda, pages=547, genes=27313, failed_pages=0。

- 2026-06-03 12:54:04 CST：阶段 4 物种完成 10/147：tax=2762, Cyanophora paradoxa, pages=495, genes=24702, failed_pages=0。

## 当前暂停状态

更新时间：2026-06-03 12:58 CST

全量分页下载已暂停，原因是 PEO 远端在长时间连续请求后开始出现连接超时、curl 35/56 断连和个别 HTTP 失败。为避免继续产生大量缺页，已停止下载进程。

当前本地状态：

- 实际占用：约 1.7 GB
- 已保存物种分页文件：6,174 个
- 已完整或基本完整下载到物种 10；物种 11 `tax=3311` 当前保存 62/827 页
- 失败页日志：`peo_download/logs/failed_species_pages.tsv`，当前 48 行
- 完整物种基因分页预估：126,786 页，约 36.25 GB

继续下载建议：

- 等远端连接恢复或低峰期再继续。
- 使用 `mamba run -n bio3 python peo_download/download_peo_data.py --workers 2` 从断点续传。
- 下载结束后需要根据 `failed_species_pages.tsv` 单独重试缺页，直到每个物种目录的 `page_*.json` 数量等于 `species_pages.summary.json` 中的 `pageTotal`。

- 2026-06-03 14:25:18 CST：阶段 4 开始：按物种分页下载完整基因索引。

- 2026-06-03 14:25:28 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655, failed_pages=0。

- 2026-06-03 14:25:38 CST：阶段 4 物种完成 2/147：tax=4081, Solanum lycopersicum, pages=682, genes=34075, failed_pages=0。

- 2026-06-03 14:25:47 CST：阶段 4 物种完成 3/147：tax=29760, Vitis vinifera, pages=527, genes=26346, failed_pages=0。

- 2026-06-03 14:25:54 CST：阶段 4 物种完成 4/147：tax=3055, Chlamydomonas reinhardtii, pages=355, genes=17741, failed_pages=0。

- 2026-06-03 14:26:04 CST：阶段 4 物种完成 5/147：tax=3218, Physcomitrella patens, pages=650, genes=32458, failed_pages=0。

- 2026-06-03 14:26:35 CST：阶段 4 物种完成 6/147：tax=3329, Picea abies, pages=1333, genes=66632, failed_pages=0。

- 2026-06-03 14:26:41 CST：阶段 4 物种完成 7/147：tax=3197, Marchantia polymorpha, pages=389, genes=19421, failed_pages=0。

- 2026-06-03 14:26:51 CST：阶段 4 物种完成 8/147：tax=88036, Selaginella moellendorffii, pages=446, genes=22285, failed_pages=0。

- 2026-06-03 14:27:04 CST：阶段 4 物种完成 9/147：tax=13333, Amborella trichopoda, pages=547, genes=27313, failed_pages=0。

- 2026-06-03 14:27:11 CST：阶段 4 物种完成 10/147：tax=2762, Cyanophora paradoxa, pages=495, genes=24702, failed_pages=0。

- 2026-06-03 15:06:02 CST：阶段 4 物种完成 11/147：tax=3311, Gingko biloba, pages=827, genes=41309, failed_pages=0。

- 2026-06-03 15:51:38 CST：阶段 4 物种完成 12/147：tax=4530, Oryza sativa, pages=844, genes=42189, failed_pages=0。

- 2026-06-03 16:49:16 CST：阶段 4 物种完成 13/147：tax=4577, Zea mays , pages=832, genes=41576, failed_pages=0。

- 2026-06-03 17:04:31 CST：阶段 4 开始：按物种分页下载完整基因索引。

- 2026-06-03 17:04:40 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655, failed_pages=0。

- 2026-06-03 17:04:52 CST：阶段 4 物种完成 2/147：tax=4081, Solanum lycopersicum, pages=682, genes=34075, failed_pages=0。

- 2026-06-03 17:05:01 CST：阶段 4 物种完成 3/147：tax=29760, Vitis vinifera, pages=527, genes=26346, failed_pages=0。

- 2026-06-03 17:05:07 CST：阶段 4 物种完成 4/147：tax=3055, Chlamydomonas reinhardtii, pages=355, genes=17741, failed_pages=0。

- 2026-06-03 17:05:17 CST：阶段 4 物种完成 5/147：tax=3218, Physcomitrella patens, pages=650, genes=32458, failed_pages=0。

- 2026-06-03 17:05:37 CST：阶段 4 物种完成 6/147：tax=3329, Picea abies, pages=1333, genes=66632, failed_pages=0。

- 2026-06-03 17:05:44 CST：阶段 4 物种完成 7/147：tax=3197, Marchantia polymorpha, pages=389, genes=19421, failed_pages=0。

- 2026-06-03 17:05:51 CST：阶段 4 物种完成 8/147：tax=88036, Selaginella moellendorffii, pages=446, genes=22285, failed_pages=0。

- 2026-06-03 17:06:00 CST：阶段 4 物种完成 9/147：tax=13333, Amborella trichopoda, pages=547, genes=27313, failed_pages=0。

- 2026-06-03 17:06:07 CST：阶段 4 物种完成 10/147：tax=2762, Cyanophora paradoxa, pages=495, genes=24702, failed_pages=0。

- 2026-06-03 17:06:21 CST：阶段 4 物种完成 11/147：tax=3311, Gingko biloba, pages=827, genes=41309, failed_pages=0。

- 2026-06-03 17:06:34 CST：阶段 4 物种完成 12/147：tax=4530, Oryza sativa, pages=844, genes=42189, failed_pages=0。

- 2026-06-03 17:06:47 CST：阶段 4 物种完成 13/147：tax=4577, Zea mays , pages=832, genes=41576, failed_pages=0。

- 2026-06-03 17:39:25 CST：阶段 4 物种完成 14/147：tax=4558, Sorghum bicolor, pages=683, genes=34129, failed_pages=0。

- 2026-06-04 01:20:13 CST：阶段 4 物种完成 15/147：tax=4565, Triticum aestivum, pages=2151, genes=107545, failed_pages=19。

- 2026-06-04 02:17:32 CST：阶段 4 物种完成 16/147：tax=3694, Populus trichocarpa, pages=859, genes=42950, failed_pages=0。

- 2026-06-04 05:53:45 CST：阶段 4 物种完成 17/147：tax=3708, Brassica napus, pages=2021, genes=101040, failed_pages=0。

- 2026-06-04 07:08:37 CST：阶段 4 物种完成 18/147：tax=3847, Glycine max, pages=1058, genes=52872, failed_pages=0。

- 2026-06-04 07:59:10 CST：阶段 4 物种完成 19/147：tax=3711, Brassica rapa, pages=810, genes=40492, failed_pages=0。

- 2026-06-04 08:45:22 CST：阶段 4 物种完成 20/147：tax=4513, Hordeum vulgare, pages=754, genes=37673, failed_pages=0。

- 2026-06-04 15:20:57 CST：阶段 4 开始：按物种分页下载完整基因索引。

- 2026-06-04 15:21:13 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655, failed_pages=0。

- 2026-06-04 15:21:32 CST：阶段 4 物种完成 2/147：tax=4081, Solanum lycopersicum, pages=682, genes=34075, failed_pages=0。

- 2026-06-04 15:21:48 CST：阶段 4 物种完成 3/147：tax=29760, Vitis vinifera, pages=527, genes=26346, failed_pages=0。

- 2026-06-04 15:21:59 CST：阶段 4 物种完成 4/147：tax=3055, Chlamydomonas reinhardtii, pages=355, genes=17741, failed_pages=0。

- 2026-06-04 15:22:17 CST：阶段 4 物种完成 5/147：tax=3218, Physcomitrella patens, pages=650, genes=32458, failed_pages=0。

- 2026-06-04 15:23:05 CST：阶段 4 开始：按物种分页下载完整基因索引。

- 2026-06-04 15:24:51 CST：阶段 4 开始：按物种分页下载完整基因索引。

- 2026-06-04 15:24:54 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655, failed_pages=0。

- 2026-06-04 15:26:08 CST：阶段 4 开始：按物种分页下载完整基因索引。

- 2026-06-04 15:26:11 CST：阶段 4 物种完成 1/147：tax=3702, Arabidopsis thaliana, pages=554, genes=27655, failed_pages=0。

- 2026-06-04 15:26:16 CST：阶段 4 物种完成 2/147：tax=4081, Solanum lycopersicum, pages=682, genes=34075, failed_pages=0。

- 2026-06-04 15:26:19 CST：阶段 4 物种完成 3/147：tax=29760, Vitis vinifera, pages=527, genes=26346, failed_pages=0。

- 2026-06-04 15:26:21 CST：阶段 4 物种完成 4/147：tax=3055, Chlamydomonas reinhardtii, pages=355, genes=17741, failed_pages=0。

- 2026-06-04 15:26:26 CST：阶段 4 物种完成 5/147：tax=3218, Physcomitrella patens, pages=650, genes=32458, failed_pages=0。

- 2026-06-04 15:26:58 CST：阶段 4 物种完成 6/147：tax=3329, Picea abies, pages=1333, genes=66632, failed_pages=0。

- 2026-06-04 15:27:10 CST：阶段 4 物种完成 7/147：tax=3197, Marchantia polymorpha, pages=389, genes=19421, failed_pages=0。

- 2026-06-04 15:27:25 CST：阶段 4 物种完成 8/147：tax=88036, Selaginella moellendorffii, pages=446, genes=22285, failed_pages=0。

- 2026-06-04 15:27:44 CST：阶段 4 物种完成 9/147：tax=13333, Amborella trichopoda, pages=547, genes=27313, failed_pages=0。

- 2026-06-04 15:27:59 CST：阶段 4 物种完成 10/147：tax=2762, Cyanophora paradoxa, pages=495, genes=24702, failed_pages=0。

- 2026-06-04 15:28:24 CST：阶段 4 物种完成 11/147：tax=3311, Gingko biloba, pages=827, genes=41309, failed_pages=0。

- 2026-06-04 15:28:49 CST：阶段 4 物种完成 12/147：tax=4530, Oryza sativa, pages=844, genes=42189, failed_pages=0。

- 2026-06-04 15:29:12 CST：阶段 4 物种完成 13/147：tax=4577, Zea mays , pages=832, genes=41576, failed_pages=0。

- 2026-06-04 15:29:32 CST：阶段 4 物种完成 14/147：tax=4558, Sorghum bicolor, pages=683, genes=34129, failed_pages=0。

- 2026-06-04 15:37:18 CST：阶段 4 物种完成 15/147：tax=4565, Triticum aestivum, pages=2151, genes=107545, failed_pages=0。

- 2026-06-04 15:37:43 CST：阶段 4 物种完成 16/147：tax=3694, Populus trichocarpa, pages=859, genes=42950, failed_pages=0。

- 2026-06-04 15:38:34 CST：阶段 4 物种完成 17/147：tax=3708, Brassica napus, pages=2021, genes=101040, failed_pages=0。

- 2026-06-04 15:39:04 CST：阶段 4 物种完成 18/147：tax=3847, Glycine max, pages=1058, genes=52872, failed_pages=0。

- 2026-06-04 15:39:26 CST：阶段 4 物种完成 19/147：tax=3711, Brassica rapa, pages=810, genes=40492, failed_pages=0。

- 2026-06-04 15:39:49 CST：阶段 4 物种完成 20/147：tax=4513, Hordeum vulgare, pages=754, genes=37673, failed_pages=0。

- 2026-06-04 17:02:19 CST：阶段 4 物种完成 21/147：tax=3635, Gossypium hirsutum, pages=1456, genes=72761, failed_pages=3。
