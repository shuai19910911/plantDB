# ZEAMAP 第一批下载记录

下载日期：2026-06-04

来源：

- CNGBdb project: `CNP0001565`
- FTP root: <https://ftp.cngb.org/pub/CNSA/data3/CNP0001565/zeamap/>
- 本地目录：`maize_ZEAMAP/`

目录规则：

- 玉米 ZEAMAP 数据统一放在 `maize_ZEAMAP/`。
- 表达矩阵放在 `maize_ZEAMAP/expression/`。
- 表型/代谢表放在 `maize_ZEAMAP/phenotype/`。
- 群体结构文件放在 `maize_ZEAMAP/population/`。

## 下载文件

| 模态 | 文件 | 大小 bytes | 行数 | SHA256 |
|---|---|---:|---:|---|
| expression | `expression/zmap_expression_ref_b73_exp.tsv` | 6705782 | 43782 | `b067b4bbfddd53a89db7da782adaeb1f5e0aa537e12693a835769ee3fc6b2366` |
| expression | `expression/zmap_expression_ref_sk_exp.tsv` | 5424304 | 43271 | `ec4fe141c4ef0c83de452034fc1647e3e03aa11a408017ba503772260fe76c73` |
| expression | `expression/HZS_genes.fmt_FPKM.results` | 3683250 | 40894 | `72ecac5d7a2e80de7ccde04b88df6df09bfe747e1d8ab9d9da806215e5ae4845` |
| expression | `expression/Mo1_only7_genes.fmt_FPKM.results` | 1436651 | 38621 | `9cff8b7b4970224994acfd3844a4397b82243442fdd87423117ce325d8a5cdae` |
| phenotype/metabolome | `phenotype/ZEAMAP_phenotype_AMP_183_known_Metabolites.xls` | 731648 | NA | `2946c37bdd710e3c930bc124054927d775369110907a605820e89eaf52a6396d` |
| phenotype | `phenotype/ZEAMAP_phenotype_AMP_agri_AA_Oil.xls` | 803840 | NA | `409b3057aad4fb6f3d1420a8f8c553680974a84c88913db8c941f49deb03c39e` |
| population | `population/amp_pca.txt` | 17016 | 507 | `bb8f9ba3e171323e609ab9c581d024db185e485987ce08a6fb6e82d06dde94d1` |
| population | `population/amp_str.txt` | 15426 | 508 | `ec70cbbc90dba5a996d1ac0a96e87a4bd8a2b4877f5fd8243886741a6d24d45c` |

## 基本校验

- 8 个目标文件均下载完成，未发现 0 字节文件。
- 两个 `.xls` 文件经 `file` 检查为 `Composite Document File V2 Document`，不是 HTML 错误页。
- `amp_pca.txt` 表头为 `sample PC1 PC2 PC3 POP`。
- `zmap_expression_ref_b73_exp.tsv` 表头第一列为 `geneID`，后续为 B73 组织/时期表达列。

## 下一步

1. 解析两个 Excel 表，导出为 TSV/CSV。
2. 抽取 expression 文件中的样本/组织列名。
3. 对齐 `amp_pca.txt`、`amp_str.txt` 和 phenotype/metabolite 表中的 accession ID。
4. 输出统一样本索引表。

