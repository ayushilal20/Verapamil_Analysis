# Verapamil Mechanism of Action in Beta Cells

## Overview

This repository provides a comprehensive analysis of **verapamil's mechanism of action in pancreatic beta cells**, with a focus on its impact on gene expression, pathway enrichment, and gene co-expression network topology. The project integrates transcriptomic data, functional enrichment (GO, KEGG, Reactome, WikiPathways), and network analysis to elucidate how verapamil modulates beta cell biology. The analysis framework adapts the structure of the [Amiloride Drug MOA study](https://github.com/evanpeikon/Amilioride_Drug_MOA), using it to amalyze the impacct of Verapamil on pancreatic beta-cell function.

## Background

Verapamil is a clinically approved L-type calcium channel blocker. Recent studies suggest it may protect pancreatic beta cells and improve glycemic control in diabetes by mechanisms beyond calcium channel inhibition. This project systematically investigates verapamil's molecular effects on beta cells, focusing on:

- **Gene expression changes**
- **Pathway and functional enrichment**
- **Gene co-expression network rewiring**

## 📂 Data Source
The dataset used is from **GEO accession [GSE230803](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE230803)** containing the precomputed differential expression result table for:
- **12 Verapamil-treated samples (V1-V12)**
- **12 Control samples (C1-C12)**
I couldn't start from creating the count matrix since the sample size was too big.
---

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

---

## Key Findings

- **Cholesterol and Sterol Biosynthesis Disruption:**  
  Verapamil strongly downregulates cholesterol/sterol biosynthesis pathways (GO, KEGG, Reactome, WikiPathways), shifting regulatory control from canonical enzymes (e.g., HMGCR) to alternative regulators (e.g., INSIG1, CYP51). This may alter membrane composition and insulin granule exocytosis, impacting beta cell function.

- **Cell Cycle and Proliferation:**  
  Enrichment of cell cycle and mitotic spindle organization pathways suggests verapamil may suppress beta cell proliferation, potentially reducing beta cell mass with chronic exposure.

- **Neuronal and Ion Channel Signaling:**  
  Pathways related to neuronal signaling (dopaminergic synapse, GABA-A receptor activity) and ion channel complexes are enriched, reflecting the shared excitability of neurons and beta cells and verapamil’s broad impact on cellular signaling.

- **Network Rewiring and Modularity:**  
  Verapamil treatment leads to:
  - Lower network density and connectivity
  - Higher modularity (more distinct functional communities)
  - Near-complete replacement of hub genes, with only ATF4 (a stress-response regulator) conserved between conditions
  - Emergence of new hubs (e.g., INSIG1, CYP51, SLC38A3) related to lipid metabolism, stress response, and membrane transport

- **Therapeutic and Adverse Implications:**  
  While verapamil may protect against lipotoxicity and ER stress, chronic disruption of cholesterol synthesis and cell cycle arrest could impair beta cell function and mass.

## Results Summary

- **Pathway Enrichment:**  
  - Strongest enrichment for cholesterol/sterol biosynthesis, cell cycle regulation, and neuronal signaling pathways.
  - Key genes: **INSIG1, CYP51, HMGCR, SLC38A3, ATF4**

- **Network Topology:**  
  - Verapamil network: 100 nodes, 1,206 edges, density 0.244, modularity 0.428, 6 communities
  - Control network: 100 nodes, 1,851 edges, density 0.374, modularity 0.179, 7 communities

- **Hub Genes:**  
  - **Verapamil-specific:** INSIG1, CYP51, SLC38A3, MFSDA2A, GLB1L2, TMEM215, TMEM51, KDR, PSAT1
  - **Control-specific:** HMGCR, DHCR7, MEST, MAFB, PLK3, ACSS2, SDF2L1, PARVB, ST8SIA2
  - **Shared:** ATF4

- **Interpretation:**  
  Verapamil induces a shift from canonical cholesterol synthesis and cell cycle hubs to stress response and membrane transport hubs, increasing network modularity and potentially enhancing beta cell resilience to metabolic stress.

## 🧬 Key Results

### 🧠 **Network Topology Shifts**
- **Verapamil network**: Lower density (0.244) and degree (avg. 24.1)
- **Control network**: Higher density (0.374), avg. degree (37.0)
- **Modularity**: Higher in Verapamil (0.428 vs. 0.179) → more compartmentalized

### 🔗 **Hub Gene Rewiring**
| Condition        | Top Hub Genes                            |
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

### 🧬 **Biological Implications**
- **Lipid Metabolism Rewiring**: Verapamil suppresses canonical HMGCR-driven cholesterol synthesis in favor of Insig1 and Cyp51.
- **Stress Adaptation**: Atf4 appears as a conserved stress hub.
- **Loss of Proliferative Signals**: Control hubs (Plk3, Mafb) vanish in Verapamil network, indicating G2/M phase arrest.

---

## ⚠️ Limitations
- DEG-based network inference excludes genes with moderate changes.
- Validation of gene function and protein activity requires wet-lab experiments.

---

## 🔧 Requirements
- Python 3.8+
- `pandas`, `numpy`, `matplotlib`, `seaborn`, `networkx`, `gseapy`, `matplotlib-venn`
# Verapamil Drug Mechanism of Action (MOA) Analysis in Type 2 Diabetes

This repository contains the complete pipeline and results for investigating the mechanism of action (MOA) of **Verapamil** in the context of **Type 2 Diabetes (T2D)** using publicly available RNA-seq data. The analysis framework replicates and extends the structure of the [Amiloride Drug MOA study](https://github.com/evanpeikon/Amilioride_Drug_MOA), adapting it to Verapamil and its impact on pancreatic beta-cell function.

---

## 🔬 Objective
To elucidate the transcriptional, regulatory, and network-level changes induced by **Verapamil**, a calcium channel blocker, in pancreatic beta cells. This study focuses on understanding how Verapamil influences:
- **Insulin secretion pathways**
- **Cholesterol/sterol biosynthesis**
- **Beta-cell survival and stress response**
- **Co-expression network rewiring**

---

## 📂 Data Source
The dataset used is from **GEO accession [GSE230803](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE230803)** containing raw count data for:
- **12 Verapamil-treated samples (V1-V12)**
- **12 Control samples (C1-C12)**

---

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

---

## 🧬 Key Results

### 🧠 **Network Topology Shifts**
- **Verapamil network**: Lower density (0.244) and degree (avg. 24.1)
- **Control network**: Higher density (0.374), avg. degree (37.0)
- **Modularity**: Higher in Verapamil (0.428 vs. 0.179) → more compartmentalized

### 🔗 **Hub Gene Rewiring**
| Condition        | Top Hub Genes                            |
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

### 🧬 **Biological Implications**
- **Lipid Metabolism Rewiring**: Verapamil suppresses canonical HMGCR-driven cholesterol synthesis in favor of Insig1 and Cyp51.
- **Stress Adaptation**: Atf4 appears as a conserved stress hub.
- **Loss of Proliferative Signals**: Control hubs (Plk3, Mafb) vanish in Verapamil network, indicating G2/M phase arrest.

---

## ⚠️ Limitations
- DEG-based network inference excludes genes with moderate changes.
- Validation of gene function and protein activity requires wet-lab experiments.

---

## 📌 Future Directions
- Validate Atf4, Cyp51, Insig1 using knockdown/overexpression models.
- Test cholesterol supplementation rescue of Verapamil-treated beta cells.
- Single-cell RNA-seq to resolve subnetwork specificity.
- Patch-clamp or Ca2+ flux assays to confirm ion channel modulation.

---

## 📜 Citation
If you use this repository, please cite it as:
> Adapted from Evan Peikon’s Amiloride MOA pipeline and extended for Verapamil in the context of type 2 diabetes. Includes differential expression, network, and enrichment analyses.

---

## 🔧 Requirements
- Python 3.8+
- `pandas`, `numpy`, `matplotlib`, `seaborn`, `networkx`, `gseapy`, `matplotlib-venn`

To install dependencies:
```bash
pip install -r requirements.txt
```

---

## 📁 Repository Structure
```
├── data/
│   └── GSE230803_RawCounts.csv.gz
├── scripts/
│   └── verapamil_pipeline.py
├── figures/
│   ├── volcano.png
│   ├── enrichment_dotplot.png
│   └── coexpression_networks.png
├── results/
│   ├── hub_genes.csv
│   └── enrichment_analysis_results.xlsx
└── README.md
```

---

## 📬 Contact
For any questions or collaboration inquiries, please reach out via GitHub issues or pull requests.



