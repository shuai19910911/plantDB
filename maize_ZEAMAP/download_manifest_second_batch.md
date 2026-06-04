# ZEAMAP 第二批建议下载记录

更新时间：2026-06-04 23:03:03 CST

来源：`/home/user/zhangzhishuai/myhermes/yumi/README.md` 中“第二批建议下载”的 ZEAMAP processed 数据。

## 下载范围

本批次按项目规则下载到 `maize_ZEAMAP/`，按数据库和组学类型分类。原始重测序 reads 不在本批次下载范围内。

| 类型 | 本地目录 | 文件数 | 本地体积 |
|---|---:|---:|---:|
| SNP annotation VCF + index | `maize_ZEAMAP/variation/` | 2 | 199M |
| DNA methylation mCG regions | `maize_ZEAMAP/epigenome/dna_methylation/01_regions/AMP_mCG_bed/` | 527 | 44M |
| DNA methylation mCHG regions | `maize_ZEAMAP/epigenome/dna_methylation/01_regions/AMP_mCHG_bed/` | 527 | 47M |
| DNA methylation mCHH regions | `maize_ZEAMAP/epigenome/dna_methylation/01_regions/AMP_mCHH_bed/` | 527 | 26M |
| DNA methylation site-level methylC | `maize_ZEAMAP/epigenome/dna_methylation/02_sites/AMP_Methyl_sites/` | 527 | 99G |
| Chromatin accessibility | `maize_ZEAMAP/epigenome/chromatin_accessibility/` | 5 | 756M |
| Chromatin interaction | `maize_ZEAMAP/epigenome/chromatin_interaction/` | 11 | 58M |

合计：2126 个文件，约 100G。

## 清单文件

- 下载 URL 清单：`maize_ZEAMAP/download_urls_second_batch.txt`
- 远端索引解析表：`maize_ZEAMAP/metadata/zeamap_second_batch_files.tsv`
- 下载日志：
  - `maize_ZEAMAP/metadata/download_second_batch.log`
  - `maize_ZEAMAP/metadata/download_second_batch_worker2.log`
- 远端目录索引快照：`maize_ZEAMAP/metadata/remote_*_index.html`

## 完整性检查

清单文件数：2126。  
本地非空文件数：2126。  
md5 校验：2118 OK，0 BAD。

| 校验目录 | OK | BAD |
|---|---:|---:|
| `AMP_Methyl_sites` | 526 | 0 |
| `AMP_mCG_bed` | 526 | 0 |
| `AMP_mCHG_bed` | 526 | 0 |
| `AMP_mCHH_bed` | 526 | 0 |
| `chromatin_accessibility` | 4 | 0 |
| `chromatin_interaction` | 10 | 0 |

VCF 文件 `AMP_SNP_anno.vcf.gz` 和 `AMP_SNP_anno.vcf.gz.tbi` 已下载为非空文件；远端该目录未在本批清单中提供 md5 文件。

## 与预训练模型的关系

这一批补齐了 ZEAMAP 中可直接下载的群体 SNP 注释、DNA 甲基化、MNase chromatin accessibility 和 chromatin interaction processed 数据。它们适合与第一批表达矩阵、表型/代谢表和群体结构文件一起，用 inbred line 或 accession 名称做跨组学样本对齐，作为作物多组学预训练模型的核心候选数据源。

本地大文件不提交到 GitHub；GitHub 只跟踪下载清单、索引快照、manifest 和项目进展文档。
