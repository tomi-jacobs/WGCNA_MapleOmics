# WGCNA Sugar Maple Transcriptomics

## Overview
This project uses Weighted Gene Co-expression Network Analysis (WGCNA) to analyze RNA-seq transcriptomic data from sugar maple (*Acer saccharum*) under different treatment conditions. The analysis identifies clusters of co-expressed genes and explores how gene expression patterns change over time.

## Conditions
Samples were collected across four time points:
- `ctrl` — Control (no treatment)
- `07d` — 7 days post-treatment
- `14d` — 14 days post-treatment
- `21d` — 21 days post-treatment

## Pipeline Summary

### 1. Differential Expression Analysis (DESeq2)
- Raw gene-level counts are loaded and filtered (minimum row sum of 80 counts across samples)
- A DESeq2 model is fit with condition as the main factor
- Results are ordered by p-value and visualized with an MA plot

### 2. Variance Stabilizing Transformation
- Variance stabilizing transformation (VST) is applied to normalize the count data
- PCA is performed to visualize sample clustering by condition
- Transformed counts are exported for downstream WGCNA analysis

### 3. WGCNA Network Construction
- Soft-thresholding power is selected by evaluating scale-free topology fit (R² ≥ 0.90)
- An adjacency matrix is constructed using the chosen soft power
- Topological Overlap Matrix (TOM) is computed to measure gene interconnectedness
- Dissimilarity (1 - TOM) is used for hierarchical clustering and module detection

## Input Files
| File | Description |
|------|-------------|
| `Gene_level_counts_sugarmaple.txt` | Raw gene-level count matrix |
| `SugarMapleSampleInfo.txt` | Sample metadata including condition labels |

## Output Files
| File | Description |
|------|-------------|
| `SMGenecountsVarStabTr.txt` | Variance-stabilized transformed count matrix |

## Dependencies
All analysis is performed in R. The following packages are required:

- `DESeq2`
- `WGCNA`
- `apeglm`
- `pheatmap`
- `ggplot2`
- `reshape2`
- `scales`
- `genefilter`
- `stringr`
- `doParallel`
- `rgl`

Install Bioconductor packages with:
```r
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install(c("DESeq2", "apeglm", "genefilter", "WGCNA"))
```

## Usage
Open `WGCNA_forMapleTranscriptomics.rmd` in RStudio and knit the document, or run each code chunk sequentially. Make sure all input files are in the same working directory as the `.rmd` file.

