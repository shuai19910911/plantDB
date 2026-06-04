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
