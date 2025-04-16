# Verapamil Mechanism of Action in Beta Cells

## Overview

This repository provides a comprehensive analysis of **verapamil's mechanism of action in pancreatic beta cells**, with a focus on its impact on gene expression, pathway enrichment, and gene co-expression network topology. The project integrates transcriptomic data, functional enrichment (GO, KEGG, Reactome, WikiPathways), and network analysis to elucidate how verapamil modulates beta cell biology. The analysis framework adapts the structure of the [Amiloride Drug MOA study](https://github.com/evanpeikon/Amilioride_Drug_MOA), to amalyze the impacct of Verapamil on pancreatic beta-cell function.

## Background

Verapamil is a clinically approved L-type calcium channel blocker. Recent studies suggest it may protect pancreatic beta cells and improve glycemic control in diabetes by mechanisms beyond calcium channel inhibition. This project systematically investigates verapamil's molecular effects on beta cells, focusing on:

- **Gene expression changes**
- **Pathway and functional enrichment**
- **Gene co-expression network rewiring**

## 📂 Data Source
The dataset used is from **GEO accession [GSE230803](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE230803)** containing the precomputed differential expression result table for:
- **12 Verapamil-treated samples (V1-V12)**
- **12 Control samples (C1-C12)**\
I couldn't start from creating the count matrix since the sample size was too big.

## 🧪 Analysis Overview

### 1. **Differential Expression Analysis (DEA)**
- Log2 fold change and adjusted p-values were calculated.
- Genes with |log2FC| > 1 and FDR < 0.05 were considered **DEGs**.

### 2. **Enrichment Analysis**
Conducted via [GSEApy](https://github.com/zqfang/GSEApy) and included:
- **GO Biological Process, Molecular Function, and Cellular Component**
- **KEGG 2019 Mouse**
- **Reactome 2022 and WikiPathways 2019 Mouse**
- **Transcription Factors (JASPAR, TF-PPI)**
- **PPI Hub Proteins**

### 3. **Network Analysis**
WGCNA-style co-expression networks were constructed using:
- Spearman correlation matrices
- Edge thresholds (|r| > 0.7)
- Network metrics: **modularity**, **clustering coefficient**, **density**
- **Hub gene** identification and **community detection** (Louvain algorithm)

### 4. **Pathway Visualization**
- Volcano plots
- Enrichment dotplots and barplots
- Heatmaps for gene-pathway association
- Venn diagrams for hub gene overlap
- Community structure plots

## 🧬 Key Results

### 🧠 **Network Topology Shifts**
- **Verapamil network**: Lower density (0.244) and degree (avg. 24.1)
- **Control network**: Higher density (0.374), avg. degree (37.0)
- **Modularity**: Higher in Verapamil (0.428 vs. 0.179) → more compartmentalized
- Near-complete replacement of hub genes, with only ATF4 (a stress-response regulator) conserved between conditions
- Emergence of new hubs (e.g., INSIG1, CYP51, SLC38A3) related to lipid metabolism, stress response, and membrane transport

### 🔗 **Hub Gene Rewiring**
| Condition        | Top Hub Genes                             |
|------------------|-------------------------------------------|
| Verapamil        | Cyp51, Insig1, Mfsd2a, Slc38a3, Kdr, Atf4 |
| Control          | Hmgcr, Dhcr7, Mafb, Mest, Acss2, Plk3     |
| Common           | Atf4                                      |

### 📈 **Top Enriched Pathways**
- **Insulin secretion** (KEGG, GO)
- **Steroid/cholesterol biosynthesis** (KEGG, GO, Reactome)
- **Cell cycle regulation** (GO:0007052, GO:1902749)
- **Ion channel signaling** (GABA-A, sodium, potassium)
- **Neuronal-like signaling** (dopaminergic synapse, nicotine addiction)
 - Key genes: **INSIG1, CYP51, HMGCR, SLC38A3, ATF4**

### 🧬 **Biological Implications**
- **Lipid Metabolism Rewiring**: Verapamil suppresses canonical HMGCR-driven cholesterol synthesis in favor of Insig1 and Cyp51.
- **Stress Adaptation**: Atf4 appears as a conserved stress hub.
- **Loss of Proliferative Signals**: Control hubs (Plk3, Mafb) vanish in Verapamil network, indicating G2/M phase arrest.

## ⚠️ Limitations
- DEG-based network inference excludes genes with moderate changes.
- Validation of gene function and protein activity requires wet-lab experiments.

## 🔧 Requirements
- Python 3.8+
- `pandas`, `numpy`, `matplotlib`, `seaborn`, `networkx`, `gseapy`, `matplotlib-venn`






