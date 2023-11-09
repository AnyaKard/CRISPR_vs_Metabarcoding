# CRISPR_vs_Metabarcoding
This repository contains all the code used to analyse freshwater macroinvertebrate bulk eDNA treated with CRISPR-Cas enrichment compared to metabarcoding to assess the use of CRISPR-Cas enrichment for quantitative estimates

1. Data cleanup
2. Reference database construction
3. VSEARCH analysis
4. Bowtie2 analysis
5. Statistical analysis
---
## 1. Data cleanup
Raw fastq files were quality trimmed using FastP v 0.23.3 (S. Chen et al., 2018) to remove adapters and low quality bases (S. Chen et al., 2018). Per-cycle quality profiles, per-cycle base contents, adapter trimming results and k-mer counts were checked to ensure trimming was successful.
[raw data quality filtering] (link to the .md code)

---
## 2. Reference database construction
To create a reference database to detect the species present in the data CRABS v 1.0.1 (G. Jeunen et al., 2023) was used (link to CRABS repo)
The reference database included mitochondrial genomes produced from the same species of individuals used to create the mock communities studied here.
[Reference Database creation] (link to the .md code)

---
## 3. VSEARCH analysis
VSEARCH is a standard approach for analysis of metabarcoding data.
The pipeline for analysis follows Gert-Jan Jeunen's pipeline with some modifications detailed in the code.

[VSEARCH pipeline] (link to the .md code)

- Sequence reads are merged using VSEARCH
- Demultiplexing is done using Cutadapt
- Quality filtering using VSEARCH with minimum length of 260, maximum length of 400 for metabarcoding and minimum length of 320, maximum length of 550 (based on predicted target lengths) for CRISPR-Cas enriched 
- Dereplication of the sequences using VSEARCH
- Clustering into OTUs using VSEARCH
- Removing chimeras for the metabarcoding data (CRISPR-Cas enrichment does not produce chimeric data) using VSEARCH
- Generate OTU table using VSEARCH
- Assign taxonomy to the OTUs using VSEARCH
  
Finally the OTU table and taxonomy where combined in excel and taxa that had a higher than 0.8 confidence threshold at the genus level where assigned to the OTU and counted towards the normalised read tables which were produced in excel and used in statisical analysis.

(picture of what the excel spreadsheet would look like)

---
## 4. Bowtie2 analysis
Bowtie2 was used to analyse the data in the original FLASH-NGS paper and so it was tested too to see if there was a large difference in the results between VSEARCH and Bowtie2.

[Bowtie2 pipeline] (link to the .md code)

- The filtered data was aligned to the reference... using Bowtie2
- The resulting sam file is filitered with SAMtools
- To tabulate the results BBMap is used

The table produced in BBMap is used to create normalised read tables which are also produced in excel and used in statisical analysis.

(picture of what the excel spreadsheet would look like)

Bowtie2 is also used to determine the amount off-target reads produced using CRISPR-Cas enrichment

[Bowtie2 off-target pipeline] (link to the .md code)

- Determined the proportion of reads that mapped between the forward and reverse guides using SAMtools to calculate the number of reads on and off target for each species.
- 

---
## 5. Statistical analysis
All statistical analyses were undertaken in R (http://www.R-project.org)







