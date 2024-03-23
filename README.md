# RNA-seq Project
Authors: Valeria Cabrera, Victoria Lelis and Ariana Silva

March, 2024

Bioinformatics course of the Licenciatura en Ciencias Genómicas, Universidad Nacional Autónoma de México, Unidad Juriquilla

Professors of bioinformatics course: Dra. Evelia Coss, Dra. Alejandra Medina

This is a repository where we describe step by step the process performed by the Pink Team during the RNA-seq Practicum.

## Overview

**1. Raw Data**

It is a folder containing scripts and explanations of the outputs of each of the steps mentioned below, you can check out it [here](https://github.com/arianaresi/RNA-seq-Project/tree/main/Raw%20data).

In addition, each of the specific steps during this process can be reviewed by clicking on the desired title:

- [Download](https://github.com/arianaresi/RNA-seq-Project/blob/main/Raw%20data/Download.md)
- [Fastqc](https://github.com/arianaresi/RNA-seq-Project/blob/main/Raw%20data/FastQC_RawData.md)
- [Multiqc](https://github.com/arianaresi/RNA-seq-Project/blob/main/Raw%20data/MultiQC_RawData.md)

**2. Trimming**

It is a folder containing scripts and explanations of the outputs of each of the steps mentioned below, you can check out it in the [Trimming directory](https://github.com/arianaresi/RNA-seq-Project/tree/main/Trimming).

In addition, each of the specific steps during the Trimming process can be reviewed by clicking on the desired title:

   - [Results](https://github.com/arianaresi/RNA-seq-Project/blob/main/Trimming/Trimming_code_and_results.md)
   - [Fastqc](https://github.com/arianaresi/RNA-seq-Project/blob/main/Trimming/FastQC_trimmed.md)
   - [Multiqc](https://github.com/arianaresi/RNA-seq-Project/blob/main/Trimming/MultiQC_trimmed.md)

**3. Alignment**

It is a folder containing scripts and explanations of the outputs of each of the steps mentioned below, you can check out it in the [Alignment directory](https://github.com/arianaresi/RNA-seq-Project/tree/main/Alignment).

   - [Definition and workflow](https://github.com/arianaresi/RNA-seq-Project/blob/main/Alignment/Definition%20and%20workflow.md)
   - [STAR index](https://github.com/arianaresi/RNA-seq-Project/blob/main/Alignment/STAR_index.md)
   - [STAR alignment](https://github.com/arianaresi/RNA-seq-Project/blob/main/Alignment/STAR_alignment.md)
  
**4. R analysis**

A single code was made for import data into R, Normalization and Batch Normalization / DEG Correction you can check out it here

   - Import STAR data to R
   - Normalization
   - Batch Normalization
   - DEG Correction (DESeq2)
  
**5. GSEA - Functional Analysis**
- Heatmap
