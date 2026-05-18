# NRF1 Promoter Motif Scanner & GO Enrichment Pipeline

This repository contains a high-throughput bioinformatics pipeline designed to map Transcription Start Sites (TSS), isolate proximal promoter regions, and identify downstream functional pathways regulated by the human transcription factor **Nuclear Respiratory Factor 1 (NRF1)**.

The analysis is executed using a hybridized architecture of string-matching Python scripts, `bedtools` coordinate manipulations, and genomic visualizations.

---

## 🧬 Project Overview

NRF1 plays a critical role in the human genome by activating the expression of key metabolic genes required for mitochondrial respiration, structural assembly of the electron transport chain, and cellular energy homeostasis. This project scans the human proximal promoter workspace to locate the consensus NRF1 structural footprint:

$$\text{5'} - \text{GCGC[ACGT][ACGT]GCGC} - \text{3'}$$

### Workflow Architecture
1. **Coordinate Compilation (`make_bed.py`)**: Parses raw Ensembl genomic annotations into standard browser extensible data (BED) structures centered on active TSS coordinates.
2. **Upstream Interval Isolation (`bedtools slop`)**: Extracts explicit $500\text{ bp}$ windows upstream of each transcription boundary relative to strand directionality ($+$ or $-$).
3. **Sequence Resolution (`bedtools getfasta`)**: Maps the resulting intervals against the `hg38` reference assembly to fetch nucleotide sequences.
4. **Motif Footprint Scanning (`find_nrf1.py`)**: Uses regular expressions to parse sequences for the conservation of the target palindromic duplex.
5. **Functional Ontology Visualization**: Computes statistical hypergeometric enrichment across Human Biological Processes (BP).

---

## 📂 Repository Structure

```text
├── human_gene_annotation.tsv.gz   # Raw Ensembl BioMart transcript model data
├── hg38.chrom.sizes               # Chromosome length layout parameters
├── make_bed.py                    # Script: Converts annotation records to BED
├── find_nrf1.py                   # Script: RegEx sequence scanner for NRF1 matrix
├── nrf1_genes.txt                 # Output: Sorted list of identified unique target genes
├── go_results.csv                 # Output: Tabulated GO enrichment metrics (p-values, q-values)
├── README.md                      # Documentation
└── [Visual Plots]                 # Output data graphics (generated from pipeline calculations)
