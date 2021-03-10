# Spatially resolved transcriptomics

Spatially resolved transcriptomics (ST) technologies allow transcriptome-wide gene expression to be measured at spatial resolution. There are several technological platforms, each with their unique advantages.


## 10x Genomics Visium

The [10x Genomics Visium](https://www.10xgenomics.com/products/spatial-gene-expression) platform measures transcriptome-wide gene expression at a two-dimensional grid of "spots" on a tissue slide. Fresh-frozen tissue is placed onto the slide, fixed, stained, and permeabilized. Each spot contains millions of spatially-barcoded capture oligonucleotides, which bind to mRNAs from the tissue. A cDNA library is then generated for sequencing, which includes the spatial barcodes, allowing reads to be mapped back to their spatial locations.

The dimensions of the tissue slide are approximately 6.5mm by 6.5mm, and contains around 5000 barcoded spots. Spots are located in a regular hexagonal arrangement, with each spot 55µm in diameter, and 100µm center to center. The number of cells per spot depends on the organism and tissue type, e.g. 0-10 for human brain, or around 50 for mouse brain. Each slide contains 4 capture areas (6.5mm x 6.5mm each). The following figure provides an illustration.

This platform is commercially available from 10x Genomics. This makes it relatively accessible, affordable, and easy for new labs to get started with, especially compared to some of the other platforms that require more specialized equipment and expertise. In our view, this makes it likely that Visium (and its future extensions) will see widespread adoption over the coming years.


<div class="figure" style="text-align: center">
<img src="images/Visium.png" alt="Schematic of 10x Genomics Visium platform. Image source: [10x Genomics Visium website](https://www.10xgenomics.com/spatial-transcriptomics/)" width="574" />
<p class="caption">(\#fig:Visium-schematic)Schematic of 10x Genomics Visium platform. Image source: [10x Genomics Visium website](https://www.10xgenomics.com/spatial-transcriptomics/)</p>
</div>



## Cartana

Cartana allows measuring expression levels of up to hundreds of targeted genes at single-cell resolution, using *in situ* sequencing. The platform was recently acquired by 10x Genomics, and will be offered as a commercial product by 10x Genomics.



## Slide-seqV2



## seqFISH



## MERFISH

