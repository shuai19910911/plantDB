# 项目记忆

## 数据下载目录规则

所有数据库下载数据必须在当前项目根目录下按“作物_数据库”分类建目录。

规则：

- 默认目录命名格式：`<crop>_<database>`，使用英文小写作物名和数据库名原始缩写/名称。
- 例子：玉米 ZEAMAP 数据下载到 `maize_ZEAMAP/`。
- 若同一作物一次涉及多个数据库，先创建作物总目录，再在其中按 `<crop>_<database>` 分类，避免项目根目录杂乱。例子：大豆数据统一放到 `soybean/soybean_SoyOmics/`、`soybean/soybean_SoyOD/`、`soybean/soybean_SoyBase/`。
- 同一数据库内部可按模态继续分子目录，例如 `expression/`、`phenotype/`、`population/`、`variation/`、`epigenome/`、`metadata/`。
- 原始 SRA/FASTQ/BAM/CRAM 不在第一阶段下载；只记录 accession 和 metadata。
- 每次下载都保留 URL 清单、文件大小/checksum 或下载状态记录。
- 小阶段完成后更新 `PROGRESS.md` 和相关文档，并推送到 GitHub。
