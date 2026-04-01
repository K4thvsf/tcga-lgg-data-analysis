# TCGA LGG Gene Expression Analysis (Reproduction Study)

This repository contains an **R / Bioconductor** workflow for exploratory analysis, normalization, differential expression testing, clustering/heatmaps, gene set enrichment analysis, and correlation with clinical variables on **TCGA Lower Grade Glioma (LGG)** expression data.

The analysis uses subtype/cluster labels from the dataset metadata (see below) and reproduces an end-to-end transcriptomics analysis pipeline.

## Dataset and subtype variable (TCGA LGG)
- Dataset: **TCGA Lower Grade Glioma (LGG)**
- Subtype/cluster variable used throughout the analysis:
  - `paper_Pan.Glioma.RNA.Expression.Cluster` (levels used in the notebook: **LGr1–LGr4**)

## Reproduction / reference paper
This repository is a **reproduction of an analysis workflow** (normalization, differential expression, clustering/heatmaps, and pathway enrichment) inspired by the TCGA molecular subtype work described in:

Verhaak RG, Hoadley KA, Purdom E, et al.; Cancer Genome Atlas Research Network.  
**Integrated genomic analysis identifies clinically relevant subtypes of glioblastoma characterized by abnormalities in PDGFRA, IDH1, EGFR, and NF1.**  
*Cancer Cell.* 2010 Jan 19;17(1):98–110. doi: **10.1016/j.ccr.2009.12.020**

> Important note: the paper above focuses on **TCGA Glioblastoma (GBM)** expression subtypes (Proneural, Neural, Classical, Mesenchymal).  
> The dataset analyzed in this repository is **TCGA LGG**, and the subtype labels used here (**LGr1–LGr4**) come from the LGG dataset metadata (`paper_Pan.Glioma.RNA.Expression.Cluster`).  
> Therefore, this repo reproduces the **analysis approach**, but specific results and subtype interpretations may differ because **LGG and GBM are distinct cohorts and disease grades**.

## Contents
- `Project NGS.Rmd` — Main R Markdown analysis
- `docs/index.html` — Rendered HTML report 

## Methods (high level)
1. Data cleaning and removal of missing/unclassified samples (where applicable)
2. Exploratory data analysis (boxplots, MA/MD plots, RLE plots, PCA)
3. GC-content bias evaluation and within-lane normalization (EDASeq)
4. Filtering low-expression genes
5. Between-sample normalization comparison (CPM, full-quantile, RLE, TMM) and selection of a suitable method
6. Differential expression analysis with **edgeR**:
   - design matrix
   - pairwise contrasts among LGr1–LGr4
   - dispersion estimation
   - GLM fitting and likelihood ratio tests
   - multiple testing correction (FDR)
7. DEG exploration (MD plots, p-value distributions)
8. Heatmap visualization and clustering
9. Gene set analysis:
   - ORA
   - KEGG enrichment
   - Reactome pathway enrichment
   - GO enrichment
   - GSEA
10. Correlation with clinical variables (including IDH status where available)

## Data (not included in this repository)
The dataset file is **not included** in this public repository (it was provided separately and is ~60 MB).

To run the analysis locally, place the file here:

- `data/TCGA-lgg.RDATA`

The R Markdown expects to load it with:

```r
load("data/TCGA-lgg.RDATA")
```

## How to run
Open the Rmd in RStudio and click **Knit**, or run:

```r
rmarkdown::render("PROJECT_NGS-10.Rmd")
```

## Requirements
- R (recommended: recent version)
- Packages used include: `omicsdata`, `EDASeq`, `edgeR`, `dplyr`, `corrplot`, `pheatmap`, `clusterProfiler`, `ReactomePA`, `enrichplot` (see the Rmd for the full list)

## License
MIT (see `LICENSE`).

