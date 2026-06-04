# plantDB 进展记录

## 2026-06-04

当前阶段：数据库调研与预训练数据源评估。

已完成：

- 建立可下载作物数据库目录：`crop_multiomics_databases.md`。
- 补充适合多组学预训练模型的数据源评估：`pretraining_dataset_assessment.md`。
- 明确第一阶段优先级：玉米 ZEAMAP、油菜 BnaOmics/BnIR、茶树 TPIA2。
- 明确当前策略：优先下载 processed matrix、VCF/GVF、annotation、metadata；原始 FASTQ/SRA/BAM/CRAM 只登记 accession，不下载。

下一步：

1. 建立 ZEAMAP、BnaOmics/BnIR、TPIA2 的下载文件清单和 metadata-only 索引。
2. 核验同一 accession/inbred line 是否能跨 variation、expression、epigenome、metabolome、phenotype 对齐。
3. 设计本地目录结构和统一样本索引表。
4. 小规模下载 processed metadata/matrix，验证模型输入格式。

### ZEAMAP 第一批下载

已按项目规则创建 `maize_ZEAMAP/`，并下载 `/home/user/zhangzhishuai/myhermes/yumi/README.md` 中“第一批建议下载”的 8 个 processed 文件：

- 4 个表达矩阵文件：`maize_ZEAMAP/expression/`
- 2 个表型/代谢表：`maize_ZEAMAP/phenotype/`
- 2 个群体结构文件：`maize_ZEAMAP/population/`

下载记录见 `maize_ZEAMAP/download_manifest_first_batch.md`。原始数据文件保留在本地，不提交到 GitHub；GitHub 只跟踪下载 URL、manifest 和项目文档。

### ZEAMAP 第二批下载

已完成 `/home/user/zhangzhishuai/myhermes/yumi/README.md` 中“第二批建议下载”的 ZEAMAP processed 数据下载，仍按 `maize_ZEAMAP/` 分类保存：

- 2 个 SNP annotation VCF/index 文件：`maize_ZEAMAP/variation/`
- 2108 个 DNA methylation processed 文件：`maize_ZEAMAP/epigenome/dna_methylation/`
- 5 个 chromatin accessibility 文件：`maize_ZEAMAP/epigenome/chromatin_accessibility/`
- 11 个 chromatin interaction 文件：`maize_ZEAMAP/epigenome/chromatin_interaction/`

合计 2126 个文件，约 100G。本批含 md5 的目录已完成校验：2118 OK，0 BAD；VCF 及其 tbi 为非空文件。下载与校验记录见 `maize_ZEAMAP/download_manifest_second_batch.md`。

下一步建议：

1. 建立 ZEAMAP accession/inbred line 统一样本索引。
2. 对齐第一批 expression、phenotype、population 与第二批 methylation/chromatin/variation 文件。
3. 先抽取小样本矩阵，验证多组学预训练输入格式。
