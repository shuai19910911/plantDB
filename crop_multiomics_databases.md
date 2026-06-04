# 可下载作物数据库目录

更新日期：2026-06-04

本目录记录当前能查到、且明确提供数据下载入口或可通过数据仓库下载的作物相关数据库。优先关注基因组、注释、转录组/表达矩阵、变异、表观组、泛基因组、比较基因组、遗传图谱、QTL/GWAS、标记和育种表型等数据。

说明：

- “直接下载”指网页、FTP、HTTP、Data Store、Download 页面、CLI 或补充文件中能直接获取处理后数据。
- “需账号/许可”指数据库可下载，但可能需要注册、登录、同意数据政策或 JGI/Kazusa/项目方授权。
- 重测序原始 FASTQ/SRA/BAM/CRAM 只登记 accession 和 metadata，不在当前阶段下载。
- 这不是封闭清单；后续每发现新的可下载作物库，继续追加到本文档。

## 综合植物/作物组学数据库

| 数据库 | 链接 | 覆盖对象 | 可下载数据 | 下载状态/备注 |
|---|---|---|---|---|
| Ensembl Plants | <https://plants.ensembl.org/info/data/ftp/index.html> | 多种植物和作物 | genome FASTA、cDNA、CDS、ncRNA、protein、GFF3/GTF、TSV/JSON、MySQL、GVF/VCF | 直接下载；推荐作为标准化主入口。 |
| Gramene | <https://news.gramene.org/ftp-download> | 禾本科和多种作物 | DNA/cDNA/protein、GFF3/GTF、GVF/VCF、pathway、gene tree、orthology、pan-genome portal 数据 | 直接下载；适合比较基因组。 |
| NCBI Datasets | <https://www.ncbi.nlm.nih.gov/datasets/> | 所有 NCBI 收录作物 | RefSeq/GenBank genome、GFF3/GTF、RNA、CDS、protein、GBFF、assembly report | 直接下载；推荐 `datasets` CLI。 |
| NCBI GenBank/Assembly/Genome | <https://www.ncbi.nlm.nih.gov/assembly/> | 所有提交到 NCBI 的作物 assembly | assembly FASTA、annotation、protein、genome report | 直接下载；适合补物种和版本。 |
| Phytozome/JGI | <https://phytozome-next.jgi.doe.gov/> | 绿色植物和多种作物 | genome、gene annotation、transcript、protein、gene family、comparative genomics | 可下载；部分数据需 JGI 账号。 |
| PLAZA | <https://bioinformatics.psb.ugent.be/plaza/> | 植物比较基因组 | protein/coding sequences、gene family、ortholog/paralog、functional annotation、GFF/FASTA | 直接下载；适合同源基因和基因家族。 |
| Plant GARDEN | <https://plantgarden.jp/> | 多种植物，含番茄、草莓、花生、大豆等 | genome、gene、marker、trait-related loci | 可下载/查询；Kazusa 体系资源。 |
| LIS: Legume Information System | <https://www.legumeinfo.org/download> | 豆科作物 | genome、annotation、expression、GWAS、QTL、markers、synteny、diversity | 直接下载；Data Store 按属/种组织。 |
| Expression Atlas | <https://www.ebi.ac.uk/gxa/download> | 多物种表达数据，含作物 | processed expression matrix、RNA-seq counts、differential expression、metadata | 直接下载；不下载原始 reads。 |
| GEO | <https://www.ncbi.nlm.nih.gov/geo/> | 多物种功能基因组 | expression matrix、supplementary files、sample metadata | 直接下载处理后数据；原始 reads 转 SRA 只登记。 |
| ArrayExpress/BioStudies | <https://www.ebi.ac.uk/biostudies/arrayexpress> | 多物种表达/功能组学 | processed expression、metadata、supplementary files | 直接下载处理后数据。 |
| CoGe | <https://genomevolution.org/coge/> | 多物种比较基因组 | genome、annotation、synteny/CoGe 分析导出 | 可导出；适合比较分析补充。 |
| Crop-GPA/Crops-DB | <https://crop-gpa.aielab.net/> | 水稻、玉米、番茄、苜蓿、大豆、小麦、谷子、油菜、棉花、高粱 | gene-phenotype associations、gene/trait tables | 可下载/开放平台；偏基因-表型关系。 |
| CropMetabolome | <https://www.cropmetabolome.com/> | 多种主要作物 | metabolome reference、crop metabolite annotations、spectra/search resources | 代谢组补充库；样本级配对需另查。 |
| Crop Composition Database | <https://foodsystems.org/resources/ccdb/> | 多种农作物 | composition traits、nutrients、anti-nutrients、secondary metabolites | 直接下载/查询；偏表型/成分，不是组学主库。 |
| Genesys PGR | <https://www.genesys-pgr.org/> | 全球作物种质资源 | accession passport data、部分表型/性状数据 | 可下载；偏种质资源和表型。 |
| GRIN-Global/NPGS | <https://npgsweb.ars-grin.gov/gringlobal/search> | 作物种质资源 | accession、passport、taxonomy、trait/evaluation data | 可下载；偏种质和表型。 |
| PGP/IPK Plant Genomics and Phenomics Research Data Repository | <https://edal.ipk-gatersleben.de/> | 植物/作物研究数据 | multi-domain plant research datasets、phenomics、genomics、supplementary data | 数据仓库型入口；需按项目筛选。 |

## 水稻

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| RAP-DB | <https://rapdb.dna.naro.go.jp/> | IRGSP/Nipponbare gene models、annotation、protein、sequence、curated genes | 水稻注释主库之一。 |
| Rice Genome Annotation Project | <http://rice.uga.edu/> | MSU/TIGR genome annotation、GFF、FASTA、protein | 旧版本研究常用。 |
| MBKbase Rice | <https://www.mbkbase.org/rice/> | Nipponbare/R498 genome、GFF、pan-gene、多个水稻 genome、VCF、expression/variation | 水稻泛基因组和变异。 |
| SNP-Seek/3K Rice | <https://snp-seek.irri.org/> | SNP/indel、3K rice accession metadata、phenotype links、download page 数据 | 变异只下载 VCF/metadata，不下载原始 reads。 |
| RPAN/3K Rice Pan-genome | <https://cgm.sjtu.edu.cn/3kricedb/index.php> | rice pan-genome、PAV、gene annotation、expression profiles | 泛基因组资源。 |
| RiceVarMap | <http://ricevarmap.ncpgr.cn/> | rice variation、SNP/indel、annotation、accession information | 变异数据库；按处理后变异下载。 |
| RiceXPro | <https://ricexpro.dna.affrc.go.jp/> | rice expression profiles、microarray/RNA expression data | 表达矩阵/查询下载。 |
| RiceFREND | <https://ricefrend.dna.affrc.go.jp/> | rice co-expression data、network data | 表达共表达资源。 |
| Oryzabase | <https://shigen.nig.ac.jp/rice/oryzabase/> | gene、mutant、trait、literature、部分下载表 | 偏遗传/功能注释。 |
| RiceENCODE | <http://glab.hzau.edu.cn/RiceENCODE/> | rice epigenome、chromatin accessibility、histone marks、transcriptome tracks | 表观组处理后 tracks 优先。 |
| funRiceGenes | <https://funricegenes.github.io/> | cloned gene、trait、functional annotation tables | 偏功能基因知识库，可下载表。 |

## 玉米

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| MaizeGDB | <https://www.maizegdb.org/download> | B73/W22/NAM/Founder genome assemblies、annotation、expression、SNP、markers、raw-data links | 玉米主库；原始 reads 只登记。 |
| ZEAMAP | <http://www.zeamap.com/> | genome assemblies、annotations、gene expression matrix、genetic variants、GWAS、population structure、epigenetic data | 多组学重点库；CNGB 有 public download project。 |
| OPTIMAS-DW | <https://pmc.ncbi.nlm.nih.gov/articles/PMC3577462/> | transcriptomics、metabolomics、ionomics、proteomics、phenomics | 多组学来自 same plant material；适合样本级配对验证。 |
| Panzea | <https://www.panzea.org/> | maize diversity、SNP/genotype、phenotype、population data | 遗传多样性和关联分析。 |
| qTeller Maize | <https://qteller.maizegdb.org/> | maize expression values、metadata、export tables | 表达查询/下载。 |
| Maize Genetics and Genomics Database resources in Gramene | <https://www.gramene.org/> | orthology、pathway、variation、genome data | 与 Gramene/Ensembl 体系关联。 |

## 小麦、大麦和其他谷物

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| GrainGenes | <https://graingenes.org/> | wheat/barley/oat/rye genome links、markers、QTL、maps、pangenome resource、downloads | 谷物遗传和组学入口。 |
| Wheat URGI/IWGSC | <https://wheat-urgi.versailles.inra.fr/> | wheat reference genome、annotation、expression、variation、markers、IWGSC data | 小麦权威入口之一。 |
| Wheat Expression Browser/expVIP | <https://www.wheat-expression.com/download> | wheat expression values、metadata、summary alignment、references、homoeologues | 直接下载表达矩阵。 |
| WheatOmics | <http://202.194.139.32/> | wheat multi-omics、expression、variation、candidate gene information | 查询和下载需按模块确认。 |
| CerealsDB | <https://www.cerealsdb.uk.net/cerealgenomics/CerealsDB/indexNEW.php> | wheat SNP、VCF、genotyping data、marker tables | 小麦 SNP/标记数据。 |
| WheatIS | <https://urgi.versailles.inra.fr/wheatis> | wheat information system、data discovery、genome/phenotype links | 数据发现入口，实际下载到各源。 |
| BARLEX/IPK barley resources | <https://apex.ipk-gatersleben.de/apex/f?p=284:10> | barley genome, gene models, markers, browser data | 大麦基因组资源。 |
| BarleyMine/Barley Genome resources | <https://ics.hutton.ac.uk/barleymine/> | barley gene annotation、genome features、functional annotation | InterMine 查询导出。 |
| Oat databases at GrainGenes | <https://graingenes.org/> | oat maps、markers、QTL、genome links | 偏遗传资源，下载入口经 GrainGenes。 |
| Rye resources at GrainGenes | <https://graingenes.org/> | rye maps、markers、genome/pangenome links | 偏遗传资源。 |

## 高粱、谷子、甘蔗和能源作物

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| SorghumBase | <https://sorghumbase.org/> | sorghum genome、annotation、gene expression、variation、QTL、pan-genome | 高粱主库。 |
| SorGSD | <https://ngdc.cncb.ac.cn/sorgsd/download> | sorghum SNP/variation annotation profiles、VCF/annotation | 变异数据库；直接下载处理后数据。 |
| SugarcaneOmics/SCOD | <https://ngdc.cncb.ac.cn/scod/download?lang=en> | sugarcane genome、gene expression、genetic variation、transcription factors | 甘蔗多组学库；有 Download 页面。 |
| Phytozome Setaria/Sorghum/Panicum | <https://phytozome-next.jgi.doe.gov/> | millet/Setaria/sorghum/switchgrass genome、annotation、protein | 需关注账号/许可。 |
| Ensembl Plants cereal genomes | <https://plants.ensembl.org/> | barley、wheat、sorghum、millet 等 genome/annotation | 标准化下载入口。 |

## 豆科作物

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| SoyBase | <https://www.soybase.org/> | soybean genome、annotation、expression、QTL、GWAS、SNP、methylation、markers | 大豆主库。 |
| SoyOmics | <https://ngdc.cncb.ac.cn/soyomics/> | soybean pan-genome、variation、transcriptome、multi-omics | 大豆泛基因组和多组学。 |
| SoyOD | <https://bis.zju.edu.cn/soyod/> | soybean genome、variation、expression、functional annotation | 大豆组学整合。 |
| SoyKB | <https://soykb.org/> | soybean genomics、transcriptomics、proteomics、metabolomics、pathways | 多组学/系统生物学资源。 |
| PeanutBase | <https://www.peanutbase.org/download/> | Arachis genome、annotation、expression、genetic data、markers、synteny、diversity | 通过 LIS Data Store 下载。 |
| Cicer Genome Portal | <https://cicer.legumeinfo.org/> | chickpea genome、annotation、expression、diversity/variation、pan-gene、synteny | LIS 体系，可下载 collections。 |
| PhaseolusMine/Phaseolus LIS | <https://mines.legumeinfo.org/phaseolusmine/> | Phaseolus genome、annotation、expression、genetics、functional annotation | 来自 LIS datastore，可查询导出。 |
| Medicago Analysis Portal | <https://medicago.legumeinfo.org/> | Medicago genome、diversity、pan-genomic resources、genetic mapping | LIS Data Store 下载。 |
| Cowpea/Vigna resources in LIS | <https://www.legumeinfo.org/download> | Vigna genome、annotation、expression、markers、QTL/GWAS、diversity | LIS Data Store 下载。 |
| Lotus resources in LIS | <https://www.legumeinfo.org/genomics/lotus/> | Lotus genome、annotation、genetic/genomic resources | LIS Data Store 下载。 |
| KnowPulse | <https://knowpulse.usask.ca/> | pulse crop genome、markers、phenotype、genotype, breeding data | 豆类育种资源；部分下载/导出。 |

## 棉花

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| CottonGen | <https://www.cottongen.org/data/download> | cotton genome FASTA/GFF3、annotation、SNP VCF、unigene、RefTran、TE、array、markers、trait tables | 棉花主库；下载页很完整。 |
| CottonFGD | <https://cottonfgd.org/> | genomic sequences、gene annotation、markers、transcriptome、population resequencing variation | 功能基因组；有 bulk download。 |
| CottonMD | <http://yanglab.hzau.edu.cn/CottonMD/> | cotton multi-omics、expression、regulatory/functional annotation | 多组学补充。 |
| CottonGVD | <https://www.frontiersin.org/articles/10.3389/fpls.2021.803736/full> | cultivated cotton genomic variation | 变异数据库；可下载变异/注释。 |

## 芸薹属和油菜

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| BRAD | <http://brassicadb.cn/> | Brassica genome、gene models、synteny、annotation、markers、variation、expression | 芸薹属主库；Resources/Download。 |
| BnaOmics | <https://bnaomics.ocri-genomics.net/download> | Brassica napus genome、pan-genome、expression、epigenome、variation | 甘蓝型油菜多组学重点库。 |
| BnPIR | <https://cbi.hzau.edu.cn/bnapus/> | Brassica napus pan-genome、gene presence/absence、genome data | 泛基因组资源；有 download。 |
| BnaGVD | <https://academic.oup.com/pcp/article/62/2/378/6064164> | Brassica napus genomic variation、SNP/indel、annotation | 变异数据库；有 Download 模块。 |
| Bolbase | <http://www.ocri-genomics.org/bolbase/> | Brassica oleracea genome/gene resources | 卷心菜/甘蓝类基因组资源。 |
| BrassicaEDB | <http://brassica.biodb.org/> | Brassica expression data | 表达数据库；需确认当前可访问性。 |

## 茄科作物

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| Sol Genomics Network | <https://solgenomics.net/genomes/> | tomato、potato、pepper、eggplant 等 genome、annotation、gene sequences、markers、phenotype、breeding data | 茄科主库；FTP/Download。 |
| SGN Tomato genome | <https://solgenomics.net/tomato/> | tomato SL/ITAG genome assembly、annotation、FASTA/GFF、JBrowse/BLAST | 番茄标准入口。 |
| Tomato Functional Genomics Database | <http://ted.bti.cornell.edu/> | tomato expression、metabolite、small RNA processed results | 功能基因组；论文说明提供 analyzed results 下载。 |
| Tomato Expression Atlas/SGN expression | <https://tea.solgenomics.net/> | tomato expression atlas | 表达数据查询/下载。 |
| SpudDB | <https://spuddb.uga.edu/> | potato DM v6.1 genome、annotation、29 potato genomes、expression across 438 samples、co-expression、syntelogs | 马铃薯重点库；有 download pages。 |
| CassavaBase | <https://cassavabase.org/> | cassava genotype、phenotype、genome/sequences、breeding trial data | 木薯育种数据库；可下载/导出。 |
| Pepper Genome Platform/PGP | <http://peppergenome.snu.ac.kr/> | pepper genome assembly、annotation、gene data | 辣椒基因组入口；需确认当前可访问性。 |
| Eggplant Genome Database/SGN Eggplant | <https://solgenomics.net/organism/Solanum_melongena/genome> | eggplant genome、annotation、FTP download | SGN 中可下载。 |
| SolPanGenomics | <https://www.solpangenomics.com/> | Solanum pan-genome、genomes、annotations、variants、expression、phenotypes | 泛基因组资源；与 SGN 关联。 |

## 葫芦科

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| Cucurbit Genomics Database/CuGenDB | <http://cucurbitgenomics.org/> | cucumber、melon、watermelon、pumpkin、squash、gourd genome、annotation、EST、maps、comparative genomics | 葫芦科主库；Download 页面。 |
| Cucumber Genome Database | <http://cucumber.genomics.org.cn/> | cucumber genome、annotation、markers | 部分内容并入/关联 CuGenDB。 |
| MELONOMICS | <https://www.melonomics.net/> | melon genome、annotation、functional data | 甜瓜资源；下载需按站点确认。 |
| MeloGene | <http://melogene.upv.es/> | melon gene/expression resources | 甜瓜基因表达/功能资源。 |
| CucurbiGen | <https://cucurbigene.upv.es/> | cucurbit gene resources | 葫芦科功能/表达资源。 |
| Melonet-DB | <http://gene.melonet-db.jp/> | melon gene expression/network data | 表达/网络资源。 |

## 蔷薇科、水果和园艺作物

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| Genome Database for Rosaceae/GDR | <https://www.rosaceae.org/> | apple、peach、strawberry、pear、cherry、rose genome、annotation、markers、QTL、trait、breeding data | 蔷薇科主库；下载和查询导出。 |
| Citrus Genome Database | <https://www.citrusgenomedb.org/> | citrus genome、annotation、markers、traits、breeding/genetic data | 柑橘主库；部分 JGI 数据需遵守 Phytozome/JGI 政策。 |
| CitGVD | <http://citgvd.cric.cn/home> | citrus SNP/indel、genomic variation | 柑橘变异数据库；有 Download。 |
| LettuceDB | <https://www.lettucedb.com/> | cultivated lettuce genome、variome、phenome、microbiome、spatial transcriptome | 莴苣多组学库；需核验批量下载入口。 |
| Kiwifruit Genome Database/KGD | <https://kiwifruitgenome.org/download> | kiwifruit genome、annotation、mRNA/protein、expression、pathway、synteny | 猕猴桃主库；Download 页面。 |
| Banana Genome Hub | <https://banana-genome-hub.southgreen.fr/> | Musa genome、annotation、omics data、comparative genomics | 香蕉主库；有 global download section。 |
| MGIS/Musa Germplasm Information System | <https://www.crop-diversity.org/mgis/> | banana germplasm accession、passport、phenotype、genotype links | 偏种质，部分数据可导出。 |
| Coffee Genome Hub | <https://coffee-genome.org/> | coffee genome、gene models、transcriptomics、markers、maps、SNP | 咖啡基因组入口。 |
| Vitis International Variety Catalogue/VIVC | <https://www.vivc.de/> | grapevine cultivar/accession、traits、passport、images | 葡萄种质/品种数据，可导出。 |
| VitisExpDB/VTCdb resources | <https://pmc.ncbi.nlm.nih.gov/articles/PMC2359749/> | grape EST、expression、co-expression | 葡萄功能基因组；需确认当前站点可访问性。 |

## 根茎类、薯类和热带作物

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| Ipomoea Genome Hub | <https://www.sweetpotao.com/download_genome.html> | sweetpotato genome FASTA、GFF3、miRNA annotation、MD5 | 甘薯基因组；直接下载。 |
| Sweetpotato Genomics Resource | <https://sweetpotato.uga.edu/> | sweetpotato genome assembly、annotation、project data | 甘薯资源；可能有预发表政策。 |
| Sweetpotato GARDEN | <https://sweetpotato-garden.kazusa.or.jp/> | sweetpotato genome/gene、cDNA/EST、variation/epigenetics annotations | Kazusa 体系资源。 |
| Ipomoea batatas Genome Browser | <http://public-genomes-ngs.molgen.mpg.de/SweetPotato/> | sweetpotato genome、gene annotation、RNA-seq、transposon data | 早期甘薯资源。 |
| YamBase | <https://www.yambase.org/> | yam/Dioscorea breeding data、genome version links | 偏育种；可导出数据。 |
| CassavaBase | <https://cassavabase.org/> | cassava phenotype、genotype、genome/sequences、trial data | 木薯也列在茄科表外，此处作为根茎类重复提醒。 |

## 茶树、油料、纤维和其他经济作物

| 数据库 | 链接 | 可下载数据 | 备注 |
|---|---|---|---|
| TPIA/TPIA2 Tea Plant Information Archive | <https://tpia.teaplants.cn/download.html> | tea genomes、gene annotation、expression、transcriptome、variation、metabolites、methylome、orthologs | 茶树多组学重点库；Download 页面。 |
| TeaPGDB | <http://eplant.njau.edu.cn/tea> | tea genome、annotation、expression resources | 茶树资源；需确认站点可访问性。 |
| TeaPVs/TeaGVD | <https://bmcplantbiol.biomedcentral.com/articles/10.1186/s12870-022-03901-5> | tea genomic variation | 变异数据库；数据来源含 TPIA/NGDC。 |
| SugarcaneOmics/SCOD | <https://ngdc.cncb.ac.cn/scod/download?lang=en> | sugarcane genome、gene expression、variation、TF | 甘蔗多组学，已在高粱/能源作物表中列出。 |
| WP-MOD | <https://www.woodyplant.com/> | woody plant genomes、transcriptomes、methylome、small RNA、degradome、epigenome | 木本植物多组学数据库，适合林木/果树扩展。 |
| PopGenIE | <https://popgenie.org/> | Populus genome、transcriptome、expression、co-expression | 林木/能源植物；FTP 可下载。 |
| ForestGEO/forest tree resources | <https://treegenesdb.org/> | forest tree genome、genetic maps、markers、phenotype links | 树木作物/林木资源，部分下载/导出。 |

## 表观组、调控和功能注释补充库

| 数据库 | 链接 | 覆盖对象 | 可下载数据 | 备注 |
|---|---|---|---|---|
| PlantTFDB | <http://planttfdb.gao-lab.org/> | 多种植物，含作物 | transcription factor sequences、family annotation、FASTA/table | 功能注释补充。 |
| PlantRegMap | <http://plantregmap.gao-lab.org/> | 多种植物 | TF binding motifs、regulatory interactions、TF annotation | 调控注释补充。 |
| PlantPAN | <http://plantpan.itps.ncku.edu.tw/> | 多种植物 | promoter、TFBS、regulatory annotation | 调控元件数据。 |
| GreenPhylDB | <https://www.greenphyl.org/> | 植物基因家族 | protein family、ortholog、phylogeny、functional annotation | 比较基因组补充。 |
| Plant Reactome | <https://plantreactome.gramene.org/> | 多种植物/作物 pathway | pathway、gene-pathway mapping | 与 Gramene 关联，可下载/导出。 |
| KEGG/MapMan/PMN PlantCyc | <https://plantcyc.org/> | 植物代谢通路 | pathway、enzyme、gene mapping | 通路注释补充；许可需注意。 |

## 原始测序仓库：只登记，不下载原始 reads

| 仓库 | 链接 | 记录内容 | 当前不下载 |
|---|---|---|---|
| NCBI SRA | <https://www.ncbi.nlm.nih.gov/sra> | BioProject、BioSample、SRA Study、SRR/ERR/DRR、Run Selector metadata、library strategy、platform、sample attributes | FASTQ、SRA、BAM、CRAM。 |
| ENA | <https://www.ebi.ac.uk/ena/browser/home> | study/sample/experiment/run accession、metadata TSV/XML、FASTQ FTP links | FASTQ、BAM、CRAM。 |
| NGDC GSA/CNSA | <https://ngdc.cncb.ac.cn/gsa/> | CRA/CRR accession、BioProject、BioSample、物种、群体、组织、测序策略 | 原始 reads 暂不下载。 |
| DDBJ DRA | <https://www.ddbj.nig.ac.jp/dra/index-e.html> | DRA study/sample/run accession 和 metadata | 原始 reads 暂不下载。 |
| CNGBdb | <https://db.cngb.org/> | CNP/CNS/CNR accession、project metadata、部分处理后数据 | 原始 reads 暂不下载；ZEAMAP 等项目可下载处理后数据。 |

## 建议的本地索引字段

| 字段 | 说明 |
|---|---|
| database | 数据库名称 |
| crop_group | 作物类群，如 cereal、legume、solanaceae、brassica、fruit、fiber、root_tuber |
| crop | 作物中文名或英文名 |
| species | 拉丁名 |
| data_type | genome、annotation、transcriptome、expression_matrix、variation、epigenome、pan-genome、phenotype、marker、QTL、GWAS、pathway、metadata |
| file_format | FASTA、GFF3、GTF、VCF、GVF、TSV、CSV、Excel、JSON、BigWig、BED、HDF5 |
| version | assembly、annotation 或数据库版本 |
| url | 下载页或数据库入口 |
| accession | assembly/BioProject/BioSample/SRA/ENA/CNGB accession |
| access_policy | direct、account_required、license_required、metadata_only、unclear |
| download_status | planned、downloaded、metadata_only、skip_raw_reads、check_access |
| note | 数据体量、账号、许可、引用、文件清单等 |

## 下一步下载建议

1. 先建立综合参考层：Ensembl Plants、Gramene、NCBI Datasets 下载 genome、GFF3/GTF、CDS、protein。
2. 再建立作物专库层：水稻、玉米、小麦、大豆、棉花、油菜、番茄/马铃薯、豆科、葫芦科、蔷薇科等按数据库下载处理后数据。
3. 表达矩阵优先下载 processed expression/count matrix 和 metadata，不下载 FASTQ。
4. 变异优先下载 VCF/GVF、样本表、群体说明；若只有重测序项目，先只记录 accession。
5. 表观组优先下载 BigWig、BED、peak、methylation table、processed matrix；原始 ChIP-seq/ATAC-seq/WGBS reads 暂不下载。
6. 对需账号资源，如 Phytozome/JGI、部分 Kazusa 或项目预发表数据，先列入 `check_access`，待确认授权后再下载。
