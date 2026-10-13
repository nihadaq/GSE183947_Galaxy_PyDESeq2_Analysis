# GSE183947_Galaxy_PyDESeq2_Analysis

# 🧬 bulk_rnaseq_galaxy_pydeseq2: Automated Bulk RNA-Seq Transcriptomics Pipeline

[![Python Version](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Galaxy Europe](https://img.shields.io/badge/Galaxy--Europe-HPC-purple.svg)](https://usegalaxy.eu/)
[![PyDESeq2](https://img.shields.io/badge/PyDESeq2-v0.4%2B-orange.svg)](https://pypi.org/project/pydeseq2/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/nihadaq?utm_source=share_via&utm_content=profile&utm_medium=member_android)

An end-to-end, cloud-native bulk RNA-Seq pipeline evaluating differential gene expression patterns in human breast cancer model samples under experimental treatment compared to untreated controls (**GEO GSE183947**).

This project bridges **Galaxy Europe's** high-performance alignment infrastructure directly with a **Google Colab** execution runtime via the **BioBlend REST API**.

---

## 📌 Workflow Architecture

```text
[ Raw SRA Reads (FASTQ) ]
 ├── Untreated Control : SRR15887221, SRR15887222, SRR15887223
 └── Experimental Tx  : SRR15887224, SRR15887225, SRR15887226
           │
           ▼
[ Galaxy Europe Cloud HPC ]
 ├── Quality Control  : FastQC
 ├── Adapter Trimming : Trimmomatic / Cutadapt
 ├── Genome Alignment : STAR Aligner (Homo sapiens GRCh38/hg38)
 ├── Quantification   : featureCounts
 └── Matrix Assembly  : Column Join (28,395 gene loci)
           │
           ▼ (BioBlend REST API Stream)
[ Google Colab / Python Environment ]
 ├── Persistent Env   : Drive Linking (/Colab_Environment/bioinfo)
 ├── Runtime Patch    : Pandas 3.0 StringDtype Compatibility
 ├── Statistical GLM  : PyDESeq2 (Size Factors, Dispersion, Wald Test)
 ├── Gene Annotation  : MyGene API (Entrez ID -> HGNC Symbols)
 └── Functional GSEA  : GSEAPy / Enrichr API (GO Biological Process)
           │
           ▼
[ Publication-Grade Visual Suite & Cloud Backup ]
 ├── Volcano Plot (adjustText Label Disambiguation)
 ├── Gene Ontology Enrichment Barplot
 └── Clustered Expression Heatmap (Seaborn Z-scores)

🔬 Experimental Dataset Details
 * GEO Accession: GSE183947
 * Organism: Homo sapiens
 * Experimental Groups: 6 Total Samples (3 Untreated Control vs. 3 Experimental Treatment)
 * SRA Sample Manifest:
   * Control: SRR15887221, SRR15887222, SRR15887223
   * Treated: SRR15887224, SRR15887225, SRR15887226
📊 Summary of Analytical Findings
| Metric | Output Value |
|---|---|
| Total Loci Evaluated | 28,395 |
| Significance Thresholds | padj < 0.05 and \vert{}\log_2\text{Fold Change}\vert{} > 1.0 |
| Total Statistically Significant DEGs | 368 |
| Upregulated Genes | 212 |
| Downregulated Genes | 156 |
| Top Enriched Clusters | Cell-cycle arrest, apoptotic signaling, HOX & IRX locus co-expression modules |
🛠️ Repository Directory Structure
bulk_rnaseq_galaxy_pydeseq2/
├── notebooks/
│   └── GSE183947_Galaxy_PyDESeq2_Analysis.ipynb  # Primary reproducible Colab notebook
├── data/
│   ├── counts_matrix.tsv                         # Un-normalized gene counts from Galaxy
│   └── GSE183947_DESeq2_results.csv              # Full statistical output table with HGNC symbols
├── assets/
│   ├── GSE183947_Volcano_Plot.png                # High-resolution Volcano Plot
│   ├── GSE183947_GO_Enrichment.png               # Gene Ontology Biological Process Barplot
│   └── GSE183947_Heatmap.png                     # Top 30 DEGs Clustered Heatmap
├── .gitignore                                    # Excludes large binaries & cache
├── requirements.txt                              # Python library dependencies
├── LICENSE                                       # MIT Open-Source License
└── README.md                                     # Project documentation

🚀 Quickstart & Reproducibility
1. Clone the Repository
git clone [https://github.com/nihadaq/bulk_rnaseq_galaxy_pydeseq2.git](https://github.com/nihadaq/bulk_rnaseq_galaxy_pydeseq2.git)
cd bulk_rnaseq_galaxy_pydeseq2

2. Install Python Dependencies
pip install -r requirements.txt

3. Run Pipeline in Google Colab
Open notebooks/GSE183947_Galaxy_PyDESeq2_Analysis.ipynb in Google Colab and run all cells sequentially.
📦 Key Dependencies
 * bioblend - Galaxy Europe REST API integration
 * pydeseq2 - Differential expression modeling via Negative Binomial GLMs
 * mygene - Gene identifier conversion (Entrez ID \rightarrow HGNC Symbol)
 * gseapy - Gene Set Enrichment Analysis & Enrichr API query
 * seaborn & matplotlib - Hierarchical clustering heatmaps and plot rendering
 * adjustText - Dynamic label collision prevention for Volcano plots
👤 Author & Contact
Nihad Adil Qadir
 * 🐙 GitHub: @nihadaq
 * 💼 LinkedIn: Nihad Adil Qadir
 * 📧 Email: nihadaq@gmail.com
📜 License
Distributed under the MIT License. See LICENSE for details.

