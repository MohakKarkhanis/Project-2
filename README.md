# Project-2
DNA Methylation Biomarker Discovery: Colon Cancer

DNA methlylation is the process which stops transcription due to addition of methly groups to the DNA chains. This addition can also act as biomarkers which further provide a brief idea on diseases especially cancers. Specific DNA methylation patterns can help to provide details on the onset or even the type of cancer along with its severity.

The [Steps Followed.docx](Steps_Followed.docx) file provides a comprehensive, step-by-step walkthrough of the entire pipeline, including code snippets and intermediate visual results. Due to the high-dimensional nature of the dataset (1.80 GB), the raw Matrix files are not hosted directly in this repository, but the extraction and processing steps are fully documented.

**Objective**
Identify DNA methylation markers distinguising healthy and diseased samples for Colon Cancer.

**Tools**
1. Language: R
2. Libraries: data.table, dplyt, openxlsx
3. Bioconductor Packages: GEOquery, minfi, limma, IlluminaHumanMethylation450kanno.ilmn12.hg19
4. Visualization: EnhancedVolcano, pheatmap, ggplot2

**Methodology**
1. Data Acquisition: Harvested high-dimensional beta-value methylation data [GSE53051](https://ftp.ncbi.nlm.nih.gov/geo/series/GSE53nnn/GSE53051/matrix/GSE53051_series_matrix.txt.gz) from the Gene Expression Omnibus (GEO). **Data Structure: Size- 1.8GBs, Unnecessary Rows from the Header: 74 | 485512 CpG sites across 220 samples**
2. Phenotypic Alignment: Mapped Sample IDs to their clinical metadata to establish binary groups _Normal vs Cancerous_ Colon tissue was selected for the primary differential analysis due to its optimal sample balance. **Dimensions before alignment (Rows x Columns) 485512 x 220 | Dimensions after alignment (Rows x Columns) 220 x 47**
3. Differential Methylation Analysis: Defined a design and contrast matrix to compare Cancer vs. Normal. Utilized limma to fit linear models and apply Empirical Bayes smoothing to calculate the Log Fold Change (logFC) and adjusted P-values. Filtered the results for both statistical significance (adj. P value) and biological significance (logFC > 0.1 = indicating >10% methylation difference). **Number of Significan DMPs (adj. P<0.05): 152910 | Number of Significant DMPs with delta beta > 0.1: 93354**
4. Visualization: Generated volcano Plots to visualize the distribution of hypermethylated and hypomethylated CpG sites and created clustered Heatmaps for the top 1001 significant DMPs to observe distinct methylation patterns between cohorts.
5. Gene Annotation: Mapped the significant, isolated CpG sites to their genomic coordinates (Chromosome, Base Pair Position) associated gene symbols (UCSC_RefGene_Name), and CpG island proximity (Island, Shore, Shelf and OpenSea).

**Results**
/ The differential analysis successfully identified **93,354 biologically and statistically significant differentially methylated probes** specific to Colon Cancer.
By annotating these probes with their specific genomic locations and relationship to CpG islands, the final exported dataset [Gene Annotations of Significant biomarkers.csv](https://github.com/MohakKarkhanis/Project-2/blob/main/Gene%20Annotation/Gene%20Annotations%20of%20Significant%20biomarkers.csv) provides a highly targeted list of potential biomarkers for further disease association and functional analysis.
