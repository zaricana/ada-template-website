# Title: Investigating the structure of COVID-19 severity: A donor-level view of single-cell RNA-sequencing data 

### Abstract. 
The original study relies on the progression from asymptomatic to mild, moderate, severe and critical COVID-19 infection based on clinical judgements for many of their analyses [1]. It isn’t obvious that RNA-sequencing data follows the same structure. We will test this assumption using donors, rather than individual cells, as the unit of analysis. Donor profiles can be constructed from RNA-sequencing data by pseudobulking each donor’s cells within defined cell types for donor-cell type pairs of interest. We will ask whether clinically determined severity emerges from these profiles and whether severity is better described as a continuous gradient or as discrete stages. The story we want to tell is where clinically determined severity and RNA-sequencing data agree, where they diverge, and why this matters for how severity is defined. 

### Research questions.
**Aim 1.** Does clinically defined severity emerge from donor profiles? Where do profiles support or contradict the assigned clinical severity, and which cell types are most informative for separating particular severity groups?

**Aim 2.** Is severity better modelled as a continuous gradient or as discrete stages? Where are neighbouring severities clearly separated, and where do they overlap, and which cell types change smoothly versus sharply between particular severity groups? 

### Methods.
**Preprocessing.** A standard pipeline was applied to the expression matrix containing 647366 cells and 24929 genes [2]. Cell types refer to those identified by the authors [1]. Cell-level filtering was first performed. Cells with fewer than 200 or over 5000 expressed genes were excluded to exclude droplets and multiplets [2]. Cells with over 10% mitochondrial reads, determined as an appropriate threshold by the authors, were also excluded [1]. This step removed 1265 cells (0.20%). Per-site doublet removal was already performed by the authors and was thus not repeated. Next, donor-level filtering was performed. Donor-cell type pairs with fewer than 10 cells were excluded. The fraction of donor-cell type pairs retained has a sharp decline up to around 10 cells per pair and a more moderate decline after that mark, indicating that pairs with fewer than 10 cells most likely represent outliers. This step removed 6081 cells (0.94%). Gene-level filtering was performed last. Genes expressed in fewer than 3 of the remaining 640020 cells were excluded, removing 690 genes (2.77%). Donor profiles were then constructed for each retained donor-cell type pair using a pseudobulk approach. Raw counts for each donor-cell type pair were first summed. The summed counts were then normalized to a library size of 10000 counts and log-transformed. 

**Exploration.** The donor profile expression matrix contains 3105 donor-cell type pairs coming from 130 donors and 46 cell-types and 24239 genes. The donors can be divided into four groups: healthy, healthy administered with LPS, non-COVID-19 severe respiratory illness, and COVID-19. COVID-19 donors were either: asymptomatic or had mild, moderate, severe or critical symptoms. We first explored the donor-level structure amongst groups and severities. Sex is roughly balanced among groups. Mild to moderate severities mostly differ between males and females. Age, however, is clearly confounded with the group, with healthy and LPS donors generally being younger. As one might expect, age is also confounded with severity to some extent: asymptomatic donors were generally younger and donors with critical symptoms were generally older, although there were no critical patients between the ages of 80 and 99. One possible explanation is that patients with critical symptoms in this age group were less likely to survive and thus to be included in the study. Site is clearly confounded with both the group and severity: London only contributed COVID-19 donors, none of which were asymptomatic, Newcastle is the only site that included LPS and non-COVID-19 severe respiratory illness groups, and Cambrigde contributed most of asymptomatic COVID-19 donors. Next, we explored the cell type-level structure. The 10 most expressed cell types make up roughly 75% of the mean cell-type composition across all groups and severities. The LPS group has a larger share of naive B cells, and, along with non-COVID-19 groups, a larger share of CD16+ NK cells. Most interestingly, rare cell types expressed in 10% or less of donors were almost exclusively contributed by critical COVID-19 donors, where they make up over 5% of the mean cell-type composition. 
 
### Proposed timeline.
**Aim 1.** The work will be completed in the next 2 weeks and shared between Maeve, Ana, and Lysa.
1. Determine the set of 2000 most highly variable genes across donors within cell types. Restrict profiles to this set. Log-ratio transform counts with a pseudocount so that all cell types are included in downstream analyses. 
2. Perform PCA. Choose the number of PCs retained by inspecting the explained variance plot. Compute the k-nearest neighbours (kNN) graph in PCA space. Perform Leiden clustering and a parameter sweep to identify the resolution optimizing clustering metrics (silhouette score and/or Davies-Bouldin index). Embed the kNN graph into a 2D space using UMAP for visual inspection. 
3. Assess agreement between clusters and severity using the adjusted Rand index. Determine which cell types separate which clusters/severity groups using pseudobulk differential expression analysis. 

**Aim 2.** The work will be completed in the following 2 weeks and shared between Nolan and Titouan.
1. Define a continuous severity axis in PCA space. Compare it with clinically determined severity. Fit severity as a continuous trend and as discrete group means. 
2. Compare the fits by cross-validated prediction. 
3. Assess separation and overlap for neighbouring severity pairs. Identify cell types that show smooth and sharp changes between severity groups.  

Work on the data story will be completed in the last 2 weeks and shared between us 5. 

### Questions.
We are unsure whether and where to apply batch correction, and where to do so. The authors used Harmony to adjust PCs by sample ID before generating the kNN graph.  
1. Several variables are confounded with  COVID-19 severity. Can correcting for these covariates be done without removing information about severity?
2. At which stage should correction be applied? Should it be applied before or after pseudobulking? 

### Bibliography.
1. Stephenson E, Reynolds G, Botting RA, et al. Single-cell multi-omics analysis of the immune response in COVID-19. Nat Med. 2021;27(5):904-916. doi:10.1038/s41591-021-01329-2. 
2. Wolf FA, Angerer P, Theis FJ. SCANPY: large-scale single-cell gene expression data analysis. Genome Biol. 2018;19(1):15. Published 2018 Feb 6. doi:10.1186/s13059-017-1382-0
