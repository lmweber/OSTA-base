# Feature selection


## Background

Chapter on feature selection, including standard single-cell methods as well as new methods developed for ST data.



## Previous steps

*Code to run steps from the previous chapters, to generate the `SpatialExperiment` object required for this chapter. For more details on each step, see the previous chapters.*


```r
# LOAD DATA

library(SpatialExperiment)
library(STexampleData)
spe <- load_data("Visium_humanDLPFC")

# QUALITY CONTROL (QC)

library(scater)
# subset to keep only spots over tissue
spe <- spe[, spatialData(spe)$in_tissue == 1]
# identify mitochondrial genes
is_mito <- grepl("(^MT-)|(^mt-)", rowData(spe)$gene_name)
# calculate per-spot QC metrics
spe <- addPerCellQC(spe, subsets = list(mito = is_mito))
# select QC thresholds
qc_lib_size <- colData(spe)$sum < 500
qc_detected <- colData(spe)$detected < 250
qc_mito <- colData(spe)$subsets_mito_percent > 30
qc_cell_count <- colData(spe)$cell_count > 12
# combined set of discarded spots
discard <- qc_lib_size | qc_detected | qc_mito | qc_cell_count
colData(spe)$discard <- discard
# filter low-quality spots
spe <- spe[, !colData(spe)$discard]

# NORMALIZATION

library(scran)
# quick clustering for pool-based size factors
set.seed(123)
qclus <- quickCluster(spe)
# calculate size factors
spe <- computeSumFactors(spe, cluster = qclus)
# calculate logcounts (log-transformed normalized counts)
spe <- logNormCounts(spe)
```



## Highly variable genes (HVGs)

We use methods from `scran` [@Lun2016] to identify a set of top highly variable genes (HVGs), which will be used to define cell types. These methods were originally developed for single-cell RNA sequencing, so here we assume that spots can be treated as equivalent to cells, and we use only molecular features (gene expression).

First, we remove mitochondrial genes, since these are very highly expressed in this dataset, and are not of biological interest.


```r
# remove mitochondrial genes
spe <- spe[!is_mito, ]
dim(spe)
```

```
## [1] 33525  3582
```


Then, apply methods from `scran`. This gives us a list of HVGs, which can be used for further downstream analyses.


```r
library(scran)

# fit mean-variance relationship
dec <- modelGeneVar(spe)

# visualize mean-variance relationship
fit <- metadata(dec)
plot(fit$mean, fit$var, 
     xlab = "mean of log-expression", ylab = "variance of log-expression")
curve(fit$trend(x), col = "dodgerblue", add = TRUE, lwd = 2)
```

<img src="feature_selection_files/figure-html/select_HVGs-1.png" width="672" />

```r
# select top HVGs
top_hvgs <- getTopHVGs(dec, prop = 0.1)
length(top_hvgs)
```

```
## [1] 1448
```



## Spatially variable genes (SVGs)

Section on alternative methods for SVGs


### SpatialDE

SpatialDE [@Svensson2018]


### SPARK

SPARK [@Sun2020]


### Moran's I statistic

Moran's I statistic


### Further methods

Further methods

