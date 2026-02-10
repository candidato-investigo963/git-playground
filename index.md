# 🧬 Transcriptomic Analysis of Human Mast Cells

![Project Status](https://img.shields.io/badge/Status-In--Progress-orange)
![Environment](https://img.shields.io/badge/Environment-Docker-blue)
![R Version](https://img.shields.io/badge/R-4.3%2B-green)

**This project consists of** the implementation of a **reproducible RNA-seq pipeline** aimed at identifying **differentially expressed genes (DEGs)** in human mast cells associated with psoriasis. It serves as a comprehensive demonstration of computational best practices, ensuring that the transition from raw sequencing data to biological discovery is transparent, scalable, and fully replicable.

---

## 📊 Project Overview

This study analyzes RNA-seq data from **human mast cells** obtained from:
- **7 healthy control samples**
- **6 psoriasis patient samples**

All samples were generated using **Illumina paired-end short-read sequencing**. The primary objective is to identify **differentially expressed genes (DEGs)** associated with psoriasis-related mast cell activity.

---

## 🚀 Analysis Workflow

### 1️⃣ Data Pre-processing & Quality Control
Raw FASTQ files were assessed and cleaned using standard bioinformatics tools via the command line:

- **FastQC**: Initial quality assessment of raw reads.
- **Trimmomatic**: Adapter removal and quality trimming.
- **MultiQC**: Aggregated quality control reporting.

---

### 2️⃣ Transcript Quantification
Transcript-level expression quantification was performed using:

- **Salmon**: High-speed pseudo-alignment approach.
- **Reference Genome**: Human transcriptome (Gencode/Ensembl).
- **Output**: `quant.sf` files per sample.

---

### 3️⃣ Statistical Analysis in R
Quantification results were imported into **R/Bioconductor** for downstream analysis:

#### 3.1 Data Import & Normalization
- **tximport**: Conversion of transcript-level quantifications into gene-level counts.
- **DESeq2 (VST)**: Variance-stabilizing transformation for downstream exploratory analysis.

#### 3.2 Exploratory Data Analysis
- **Principal Component Analysis (PCA)**:  
  Used to identify sample outliers, batch effects, and global expression patterns, ensuring minimal intra-condition variability and maximal separation between biological conditions.

#### 3.3 Differential Expression Analysis
- **DESeq2**:  
  Identification of differentially expressed genes (DEGs) between psoriasis and healthy samples.

Primary significance thresholds:
- |log2 Fold Change| ≥ 2  
- Adjusted p-value ≤ 0.05

#### 3.4 Visualization & Biomarker Selection
- **EnhancedVolcano**: Generation of publication-ready volcano plots.
- **MA Plot**: Visualization of expression changes across abundance levels.

A high-stringency biomarker subset was defined using:
- |log2 Fold Change| ≥ 4  
- Adjusted p-value ≤ 1e-6  

This filtering resulted in **17 candidate biomarker genes**.

---

## 🛠️ Computational Environment

To ensure full reproducibility, the analysis environment is containerized:

- **Base Environment**: Bioconductor 3.18 / R 4.3.
- **System Dependencies**: OpenJDK 17 (for FastQC/Nextflow compatibility), Curl, and Git.
- **R Stack**: `tximport`, `DESeq2`, `EnhancedVolcano`, `clusterProfiler`, `pheatmap`, and `tidyverse`.

📦 [Access the Dockerfile](./docker/Dockerfile)

---

## 📂 Project Status & Next Steps

### 🔄 In Progress
- [ ] Gene Ontology (GO) and KEGG enrichment analysis
- [ ] GSEA (Gene Set Enrichment Analysis)
- [ ] Interactive Volcano Plot (using `plotly`)

