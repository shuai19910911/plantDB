# 大豆数据下载记录

更新时间：2026-06-05 02:34:01 CST

本批次按项目规则将大豆数据下载到 `soybean_<database>/` 目录。严格跳过大豆重测序原始数据：未下载 FASTQ、SRA、BAM、CRAM；SoyOD 的 variation 文件为数据库提供的 processed SNP/INDEL zip。

## 数据源

| 数据库 | 本地目录 | 处理方式 |
|---|---|---|
| SoyOmics | `soybean_SoyOmics/` | 下载 Download 页面提供的 genome、gene、mRNA、CDS、protein、ncRNA、repeat processed 文件。 |
| SoyOD | `soybean_SoyOD/` | 下载 TF、TE、GO/KEGG/PFAM annotation 和 processed SNP/INDEL variation zip；保存 transcriptome、population、phenome AJAX metadata。 |
| SoyBase | `soybean_SoyBase/` | 保存主页和 Glycine datastore 入口快照；未下载重测序项目原始 reads。 |

## 下载结果

清单文件：`soybean_download_urls.tsv`、`soybean_download_urls.txt`。  
跳过原始 reads 说明：`soybean_skip_raw_resequencing.tsv`。  
下载日志：`soybean_download.log`、`soybean_download_retry1.log`。  
最终缺失清单：`soybean_missing_final.tsv`，当前为空。

| 数据库 | 类型 | 文件数 |
|---|---:|---:|
| SoyOmics | genome | 36 |
| SoyOmics | gene | 36 |
| SoyOmics | mRNA | 30 |
| SoyOmics | CDS | 36 |
| SoyOmics | protein | 36 |
| SoyOmics | ncRNA | 27 |
| SoyOmics | repeat | 27 |
| SoyOD | TF annotation | 52 |
| SoyOD | TE annotation | 56 |
| SoyOD | GO/KEGG/PFAM annotation | 156 |
| SoyOD | processed variation zip | 2 |

合计：494 个清单内文件，全部为非空本地文件。

## 本地体积

| 目录 | 体积 |
|---|---:|
| `soybean_SoyOmics/` | 13G |
| `soybean_SoyOD/` | 4.7G |
| `soybean_SoyOmics/genome/` | 9.7G |
| `soybean_SoyOmics/gene/` | 417M |
| `soybean_SoyOmics/mRNA/` | 934M |
| `soybean_SoyOmics/cds/` | 726M |
| `soybean_SoyOmics/protein/` | 459M |
| `soybean_SoyOmics/ncRNA/` | 2.6M |
| `soybean_SoyOmics/repeat/` | 199M |
| `soybean_SoyOD/TF/` | 931K |
| `soybean_SoyOD/TE/` | 3.7G |
| `soybean_SoyOD/annotation/` | 973M |
| `soybean_SoyOD/variation/` | 48M |

## 完整性检查

- 清单非空文件检查：494/494。
- SoyOmics `.gz` 文件：`gzip -t` 通过，`soybean_gzip_test.log` 为空。
- SoyOD `.zip` 文件：`unzip -tqq` 通过，`soybean_zip_test.log` 为空。
- SoyOD 页面中 3 个 TE 文件名与实际远端文件名不一致，已改用可访问文件名：
  - `Zhong_Huang_13_T2T.TEanno` -> `ZH13_T2T.TEanno`
  - `Zhong_Huang_13.a1.v1.TEanno` -> `Zhong_Huang_13.v1.TEanno`
  - `Zhong_Huang_13.a2.v1.TEanno` -> `Zhong_Huang_13.v2.TEanno`

## 对建模的用途

SoyOmics 本批数据适合构建大豆 reference/pangenome 序列和 gene-level annotation 底座；SoyOD 本批数据补充 TF、TE、GO、KEGG、PFAM、population、phenome、transcriptome metadata 和 processed variation。下一步应先建立 accession/gene ID 统一索引，再判断 SoyOD population/phenome/variation 与 SoyOmics accession 是否能对齐。
