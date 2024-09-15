# Enhancer-Gene Structure Analysis with ABC Model in Alzheimer's Disease

This project focuses on analyzing enhancer-gene structures in Alzheimer's disease(AD) using [Activity-by-contrast(ABC) model](https://github.com/broadinstitute/ABC-Enhancer-Gene-Prediction). The results include original data processing, result generation, and visualization of key findings.

## Directory Structure

   (All the raw data and results can be found in the server of ISTBI, under /public/home/liuxy/final_results)
-   `raw_data/`: Contains the raw data files used for the analysis.
-   `raw_results/`: Includes the original results generated by the ABC model.
-   `data_preparation.xlsx`: Contains the data inclusion criteria for the analysis.
-   `statistics.xlsx`: Shows the preliminary statistical results of enhancer-gene pairs across different tissues.
-   `visualizations/`: Stores the visual representations of the results.
-   `README.md`: This file provides an overview of the project and usage instructions.

## References

-   Fulco, Charles P., et al. Activity-by-contact model of enhancer--promoter regulation from thousands of CRISPR perturbations. Nature genetics 51.12 (2019): 1664-1669.
-   Nasser, Joseph, et al. Genome-wide enhancer maps link risk variants to disease genes. Nature 593.7858 (2021): 238-243.

## Research story

在老师确定"variant-gene-disease"的思路之后，由其中的小部分延展成我的任务：利用ABC（Activity-by-contact）计算工具，分析各脑区的基因调控。 首先寻找不同脑区的accessibility数据，一共找到21个位置的DNase-seq或ATAC-seq。从平台下载数据后，有的格式并不符合ABC的输入格式，于是学习如何处理各种格式转化。主要是ATAC-seq要求的TagAlign格式在数据库中并不很常见，往往要从sra、fastq、bam、bed或bedpe转成。21个样本中只有5个加上了Hi-C输入，因为Encode上的Hi-C数据并不多。我尝试在其他平台下载，但一般都是sra或fastq的原始数据，还要进一步处理成ABC接受的 .hic格式。这其中我尝试了juicer软件，也确实生成了.hic为后缀的Hi-C文件，但是ABC计算时报错。调试了一段时间无果，就先放弃了。截至7月中旬，基本完成原始结果的生成和整理，总结了数据纳入标准和预测结果的初步统计。

八月份开始利用ABC results中的predictions，做进一步分析。首先考虑增强子-基因对本身，想到可以看看阿尔兹海默症显著关联的基因的增强子情况，于是从文章中找到107个AD风险基因，统计了它们在不同组织样本中对应的的增强子以及相应的ABC.score。接下来在GTEx的54个人体组织中发现6个与我选择的样本重叠的脑组织，统计了每个样本表达量top50的基因的组织特异性。然后，通过收集阿尔茨海默症显著关联SNP，取不在基因上且与每个组织enhancer有交集者，找到enhancer对应的基因，共80个，得到其在各组织以及不同脑区发育阶段的表达差异情况。最后，进行Go富集分析，前景基因为上述SNP-enhancer-gene通路确定的基因，得到这组基因在生物功能或疾病机制中的可能作用。
