# This repository is for the manuscript of Lim at all 
Citation (click the image): 
[![image](https://github.com/user-attachments/assets/c15a5a15-1fd7-4987-8e3d-9f4be2cc1c30)](https://www.embopress.org/doi/full/10.1038/s44318-024-00328-6)

### Interactive data browser
[CZ Cellxgene](https://cellxgene.cziscience.com/collections/92db8a7e-8761-4317-873f-15606c016ce5)
[![image](https://github.com/user-attachments/assets/40fcd8c0-8365-45ec-a56e-5a2cb76b8929)](https://cellxgene.cziscience.com/collections/92db8a7e-8761-4317-873f-15606c016ce5)


### Software versions

  - STAR v2.7.10a_alpha_220818
  - salmon v1.10.0
  - samtools v1.15.1
  - bcftools v1.15.1
  - cellsnp-lite v1.2.3
  - souporcell v2.5
  - featureCounts v2.0.2
  - RSEM v1.3.1

### Bulk RNA-seq processing 

A `STAR` reference genome index identical to `Cell Ranger`'s reference `2020-A` was created using the protocol described [here](https://support.10xgenomics.com/single-cell-gene-expression/software/release-notes/build#GRCh38_2020A). Following this, 4 bulk RNA-seq samples were mapped using `STAR` and quantified using `salmon`, `featureCounts`, and `RSEM`. All the commands used to map and quantify the data are contained in  `star_bulk.sh`. Quality control was done using `bulk_QC.sh`, and expression tables were created using `make_expression_tables.sh`. 

All the scripts used for bulk RNA-seq processing are available in [/bulk](https://github.com/brianpenghe/2024_AT2_organoids/tree/main/bulk).

### Variant calling from bulk RNA-seq data

Using the obtained genomic BAM files, variant calling was performed using `cellsnp-lite`. In accordance with recommendations, the variants were filtered [using common variants from the 1000 Genomes project](https://github.com/single-cell-genetics/cellSNP?tab=readme-ov-file#list-of-candidate-snps).

The variants were the combined into a merged VCF using `bcftools`: 

```
bcftools merge --threads 16 -0 *.cellsnp.out/cellSNP.cells.vcf.gz > merged.vcf
```

All the scripts used for bulk RNA-seq variant calling, as well as the outputs, are available in [/cellsnp-lite](https://github.com/brianpenghe/2024_AT2_organoids/tree/main/cellsnp-lite).

### Mapping and quantification of the multiplexed organoid scRNA-seq experiment

The multiplexed experiment was aligned and quantified using `STARsolo`. All the scripts used to run STARsolo and quality-control the outputs are available in [/starsolo](https://github.com/brianpenghe/2024_AT2_organoids/tree/main/starsolo). 

### Demultiplexing of the organoid scRNA-seq experiment

We have used `souporcell` with known genotypes (`merged.vcf` file obtained above) to de-multiplex the scRNA-seq data. 

All the scripts used to run STARsolo and quality-control the outputs are available in [/souporcell](https://github.com/brianpenghe/2024_AT2_organoids/tree/main/souporcell). 
