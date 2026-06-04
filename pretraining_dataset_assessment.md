# 作物多组学预训练模型数据源评估

更新日期：2026-06-04

目标：构建作物多组学预训练模型。可以先做单作物模型，也可以逐步扩展到泛作物模型。理想样本是同一 accession、inbred line、germplasm、cultivar 或 tissue/timepoint 同时具有多种组学，例如 genotype/variation、transcriptome、epigenome、metabolome、phenotype。

## 结论

最适合从单作物开始的数据库：

1. **ZEAMAP/玉米**：最优先。明确包含同一玉米自交系面板上的多组学数据，包括参考基因组、注释、转录组、开放染色质、染色质互作、高质量变异、表型、代谢组、遗传图谱、群体结构和 DNA 甲基化。适合做 accession-level 多模态预训练。
2. **BnaOmics/BnIR/油菜**：第二优先。整合甘蓝型油菜 pan-genome、genomics、transcriptomics、variomics、epigenomics、phenomics、metabolomics，并有 download 页面。适合做油菜多模态预训练或变异-表达-表型建模。
3. **TPIA2/茶树**：第三优先。包含多个茶树基因组、表达、转录组、350 个 accessions 的变异、107 个 Camellia 物种/材料的代谢物、DNA methylome、orthologs。适合做茶树/山茶属多组学模型，但同一样本跨全部模态的配对程度需要下载 metadata 后核验。
4. **SoyOmics/SoyBase/SoyOD/大豆**：适合大豆模型。泛基因组、变异、转录组和功能注释较强；是否存在大规模同一样本配对的代谢组/表观组需要进一步核验。
5. **SNP-Seek/MBKbase/RiceENCODE/RiceXPro/水稻组合**：水稻数据量很大，但常分散在不同数据库。适合用 accession/gene/tissue 做弱配对或分阶段预训练，不如 ZEAMAP 那样天然统一。

不建议第一阶段作为主训练集的数据库：

- Ensembl Plants、Gramene、NCBI Datasets、Phytozome、PLAZA：非常适合做参考基因组、注释、同源基因、通路和基因序列底座，但不是样本级多组学配对数据主来源。
- SRA/ENA/GSA/DRA：只适合登记 accession 和 metadata。原始 reads 体量大、处理成本高，当前阶段不下载。
- 单一表达库、单一变异库、QTL/marker 库：可作为辅助任务或标签来源，但不能单独支撑多组学预训练。

## 适配度分级


| 等级  | 含义                                | 适合任务                                       |
| --- | --------------------------------- | ------------------------------------------ |
| A   | 同一批样本/accessions 上有多种组学，且有处理后数据下载 | 多模态预训练、跨组学补全、表型预测、masked modality modeling |
| B   | 多组学丰富，但样本配对需要靠 metadata 对齐        | 弱配对预训练、分模态预训练后对齐、迁移学习                      |
| C   | 主要是单模态或参考数据                       | 参考底座、tokenizer/annotation、辅助监督标签           |


## 第一梯队：最适合直接推进


| 作物  | 数据库        | 等级  | 可用模态                                                                                                                                          | 为什么适合                                                                                          | 主要风险                              |
| --- | ---------- | --- | --------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | --------------------------------- |
| 玉米  | ZEAMAP     | A   | genome、annotation、variation、transcriptome、open chromatin、chromatin interaction、DNA methylation、metabolome、phenotype、population structure、GWAS | 文献明确说明多组学来自同一玉米自交系面板；非常适合把 accession 作为样本单位做多模态预训练                                             | 需要确认批量下载入口、文件格式和 accession ID 一致性 |
| 油菜  | BnaOmics   | A/B | pan-genome、genome、annotation、variation、transcriptome、epigenome、phenotype、population                                                           | 有明确 download 页面，模块包括 genomics、variations、transcriptomics、epigenomics、phenotypes、populations    | 不同模态是否同一批 accession 需核验           |
| 油菜  | BnIR       | A/B | genomics、epigenomics、transcriptomics、metabolomics、phenomics                                                                                   | 明确是 Brassica napus multi-omics database，强调 variation-gene expression-phenotype associations    | 入口和下载稳定性需核验；可能与 BnaOmics 有重叠      |
| 茶树  | TPIA2      | B   | genome、annotation、expression、transcriptome、variation、metabolites、methylome、orthologs                                                          | 数据类型非常全，含 350 diverse tea accessions 的变异、116/176 transcriptomes、107 Camellia 代谢物、DNA methylome | 样本级全模态配对可能不完整，需要先建 metadata map   |
| 玉米  | OPTIMAS-DW | A/B | transcriptomics、metabolomics、ionomics、proteomics、phenomics                                                                                    | 文献说明多种组学来自 same plant material，适合小规模强配对模型验证                                                    | 数据较老，覆盖规模和下载格式需核验                 |


## 第二梯队：适合扩展或弱配对训练


| 作物  | 数据库                                          | 等级  | 可用模态                                                            | 适合用法                                     | 风险                                       |
| --- | -------------------------------------------- | --- | --------------------------------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| 大豆  | SoyOmics                                     | B   | pan-genome、variation、transcriptome、multi-omics                  | 大豆单作物模型；泛基因组/变异/表达联合训练                   | 样本配对程度需下载 metadata 后确认                   |
| 大豆  | SoyBase/SoyOD/SoyKB                          | B/C | genome、annotation、expression、QTL/GWAS、SNP、methylation、pathway   | 与 SoyOmics 组合，补功能注释、QTL、GWAS、通路标签        | 多库 ID 对齐工作量较大                            |
| 水稻  | MBKbase + SNP-Seek + RiceXPro + RiceENCODE   | B   | pan-genome、variation、expression、epigenome、trait/gene annotation | 水稻数据量大，适合构建“多来源弱配对”模型                    | 数据分散；同一 accession/tissue/timepoint 配对不稳定 |
| 小麦  | Wheat URGI + expVIP + CerealsDB + GrainGenes | B/C | genome、annotation、expression、SNP、markers、QTL                    | 适合表达-基因组注释-标记/QTL 模型，尤其 gene-level 任务    | 多倍体同源基因、版本和 ID 映射复杂                      |
| 棉花  | CottonGen + CottonFGD + CottonMD             | B   | genome、annotation、variation、expression、markers、traits           | 棉花功能基因组和育种标签丰富                           | 同一样本多模态配对需核验                             |
| 马铃薯 | SpudDB                                       | B/C | genome、annotation、expression、co-expression、syntelogs、多 genome   | 适合 gene-level/gene-family 表达预训练和马铃薯单作物模型 | 多模态少于 ZEAMAP/BnaOmics                    |
| 莴苣  | LettuceDB                                    | B   | genome、variome、phenome、microbiome、spatial transcriptome         | 适合空间转录组和变异/表型扩展                          | 是否易批量下载和样本配对需核验                          |


## 第三梯队：主要作为参考底座或辅助标签


| 数据库                            | 等级  | 主要用途                                                        |
| ------------------------------ | --- | ----------------------------------------------------------- |
| Ensembl Plants                 | C   | 标准化 genome、gene annotation、CDS/protein、GFF3/GTF、ortholog 底座 |
| Gramene                        | C   | 比较基因组、pathway、orthology、variation、pan-genome portal 辅助      |
| NCBI Datasets                  | C   | 补齐物种参考基因组、注释、assembly metadata                              |
| Phytozome/JGI                  | C   | 植物 genome、annotation、gene family、比较基因组；需账号                  |
| PLAZA                          | C   | ortholog/paralog、gene family、functional annotation          |
| PlantTFDB/PlantRegMap/PlantPAN | C   | TF、调控元件、motif 和调控网络辅助标签                                     |
| Plant Reactome/PlantCyc        | C   | pathway 标签和代谢通路监督任务                                         |
| CropMetabolome                 | C/B | 作物代谢物参考库；可补代谢组模态，但样本级配对需另查                                  |


## 推荐建模路线

### 路线 1：先做单作物强配对模型

优先选 **玉米 ZEAMAP**。

样本单位：maize inbred line/accession。

候选模态：

- genotype/variation：SNP/indel/structural variants。
- transcriptome：gene expression matrix。
- epigenome：DNA methylation、open chromatin、chromatin interaction。
- metabolome：metabolite abundance。
- phenotype：agronomic traits/GWAS traits。
- annotation：gene function、pathway、ortholog、TF/motif。

预训练任务：

- masked modality modeling：遮掉表达/代谢/表型，用变异和表观组预测。
- cross-modal contrastive learning：同一 accession 的不同模态拉近，不同 accession 拉远。
- gene-context prediction：用 gene annotation、cis-regulatory features、expression jointly 预训练 gene embeddings。
- phenotype-aware pretraining：用表型作为弱监督或多任务目标。

### 路线 2：油菜多组学模型

优先组合 **BnaOmics + BnIR + BnaGVD + BRAD**。

优势：

- pan-genome、variation、transcriptome、epigenome、phenotype/metabolome 资源较集中。
- 适合做 variation-gene expression-phenotype 关联预训练。

风险：

- 需要先核验各模态 accession ID 是否一致。
- 如果 BnaOmics 与 BnIR 数据重叠，要去重并保留来源字段。

### 路线 3：泛作物基础模型

先用综合库构建 gene/species/reference 层，再接入单作物多组学库。

底座数据：

- Ensembl Plants、Gramene、NCBI Datasets、Phytozome、PLAZA。

多组学作物节点：

- 玉米 ZEAMAP。
- 油菜 BnaOmics/BnIR。
- 茶树 TPIA2。
- 大豆 SoyOmics/SoyBase。
- 水稻 MBKbase/SNP-Seek/RiceENCODE/RiceXPro。
- 棉花 CottonGen/CottonFGD。

关键技术问题：

- 统一 ID：species、accession、sample、tissue、gene、genome version。
- 统一坐标：同一作物内不同 assembly 的 liftover 或 gene orthology。
- 缺失模态：多数样本不会有全部组学，需要支持 missing-modality training。
- 数据规模：原始 reads 不下载，优先使用处理后矩阵、VCF、BED/BigWig、表型表。

## 第一阶段行动清单

1. 为 ZEAMAP、BnaOmics/BnIR、TPIA2 分别建立 `metadata_only` 清单，先抓取下载页、文件列表、模态、样本 ID。
2. 建立统一索引表字段：`database`, `crop`, `species`, `sample_id`, `accession_id`, `tissue`, `development_stage`, `treatment`, `omics_type`, `file_format`, `url`, `access_policy`, `raw_reads_flag`。
3. 只下载小型 metadata 和 processed matrix；不下载 SRA/FASTQ。
4. 先用 ZEAMAP 做可行性验证：检查同一 inbred line 是否能同时连接 variation、expression、methylation、metabolite、phenotype。
5. 若 ZEAMAP 配对成功，再扩展油菜 BnaOmics/BnIR；最后整合茶树和大豆。

## 当前需要优先核验的下载入口


| 数据库                         | 下载入口/来源                                                                                    | 核验内容                                                                                          |
| --------------------------- | ------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------- |
| ZEAMAP                      | [http://www.zeamap.com/](http://www.zeamap.com/)；CNGBdb ZEAMAP public download project     | 文件列表、processed matrix、样本 ID、是否无需登录                                                            |
| BnaOmics                    | [https://bnaomics.ocri-genomics.net/download](https://bnaomics.ocri-genomics.net/download) | pan-genome、variation、expression、epigenome、phenotype 文件和 accession 对齐                          |
| BnIR                        | [https://yanglab.hzau.edu.cn/](https://yanglab.hzau.edu.cn/)                               | 下载入口、metabolomics/phenomics 文件、是否与 BnaOmics 重复                                                |
| TPIA2                       | [https://tpia.teaplants.cn/download.html](https://tpia.teaplants.cn/download.html)         | variation 350 accessions、metabolites 107 Camellia、methylome 15/17 samples、expression metadata |
| SoyOmics                    | [https://ngdc.cncb.ac.cn/soyomics/](https://ngdc.cncb.ac.cn/soyomics/)                     | pan-genome、variation、transcriptome 的 accession 对齐                                             |
| MBKbase/SNP-Seek/RiceENCODE | 各数据库 Download 页面                                                                           | rice accession/tissue/timepoint ID 是否可对齐                                                      |


## 来源线索

- ZEAMAP 文献和页面说明其整合多个参考基因组、注释、比较基因组、转录组、开放染色质、染色质互作、高质量变异、表型、代谢组、遗传图谱、群体结构和 DNA 甲基化，并强调这些多组学来自同一玉米自交系面板。
- BnaOmics 页面说明其整合甘蓝型油菜 reference genome assemblies、annotations、gene expressions、epigenome、variations、phenotypes、populations、transcriptomics、epigenomics。
- TPIA2 文献和页面说明其整合 10 个 Camellia genomes、350 diverse tea accessions 的 SNP/indel、116/176 transcriptomes、107 Camellia 的代谢物、DNA methylome、orthologs 和 functional annotation。
- OPTIMAS-DW 文献说明 maize transcriptomic、metabolomic、ionomic、proteomic、phenomic parameters measured from the same plant material。

