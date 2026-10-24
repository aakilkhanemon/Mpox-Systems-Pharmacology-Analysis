# Systems Pharmacology & Network Topology Framework for Tri-Modal Mpox Therapeutics

[![ChemRxiv](https://img.shields.io/badge/ChemRxiv-10.26434%2Fchemrxiv.15003736%2Fv1-b31b1b.svg)](https://doi.org/10.26434/chemrxiv.15003736/v1)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python: 3.10+](https://img.shields.io/badge/Python-3.10%2B-brightgreen.svg)](https://www.python.org/)
[![NetworkX](https://img.shields.io/badge/NetworkX-3.0%2B-orange.svg)](https://networkx.org/)

<p align="center">
  <img src="assets/network_graphical_abstract.png" alt="Tri-Modal Network Pharmacology Graphical Abstract" width="100%">
</p>

Official implementation of the systems pharmacology and topological interactome framework from:  
**"System Pharmacology-Driven Tri-Modal Leads Discovery of Anti-Mpox Therapeutics: Integrating Quantum Mechanics, Molecular Dynamics, and Network Topology"**  
*Mohammed Emon, Noimul Hasan Siddiquee, Kripa Barman, Md. Enamul Haque* (ChemRxiv preprint doi: [10.26434/chemrxiv.15003736/v1](https://doi.org/10.26434/chemrxiv.15003736/v1)).

---

## The Tri-Modal Division of Labor

Traditional Mpox drug discovery focuses exclusively on viral replication inhibition while failing to resolve viral egress or severe host-driven immunopathology[cite: 39]. This pipeline reconstructs a multi-stage host-pathogen intervention across three functionally distinct modes:

1. **Mode 1: Viral-Host Egress & Cytoskeletal Modulation (Lead 1)**  
   - **Mechanism:** Targets the host `ABL1/SRC-RHOA` and `AKT1/PIK3CA` kinase signaling axes[cite: 42, 49]. Decouples virions from the host actin-tail propulsion machinery to prevent cell-to-cell spread[cite: 42, 49].
   - **Key Hubs:** AKT1 ($k=10, C_b=0.329$), PIK3CA ($k=8$), SRC ($k=8$), EGFR ($k=8, C_b=0.221$).

2. **Mode 2: Innate Immune Priming & Viral Sensing (Lead 2)**  
   - **Mechanism:** Targets the `TLR9/GSK3B` endosomal signaling hub[cite: 42, 49]. Enhances the host's intrinsic recognition of foreign poxviral dsDNA to counteract viral immune-evasion tactics[cite: 42, 49].
   - **Key Hubs:** TLR9, GSK3B, HCRTR1/2, GRM1/5[cite: 50].

3. **Mode 3: Symptomatic Inflammasome & Pain Attenuation (Lead 3)**  
   - **Mechanism:** Suppresses the `P2RX7-NLRP3` inflammasome cascade to prevent cytokine storming and tissue necrosis while simultaneously inhibiting voltage-gated sodium channels (`SCN9A`) and `TRPV1` to manage severe neuropathic lesion pain[cite: 39, 42].
   - **Key Hubs:** MYD88 ($k=11$), TNF ($k=11$), IL1B ($k=11$), CASP1 ($k=9, C_b=0.065$), NLRP3 ($k=8$), P2RX7, SCN9A.

---

## Directory Layout

```text
├── assets/                  # Graphical abstract and interactome diagrams
├── data/
│   ├── targets/             # JSON and plaintext target lists for Leads 1, 2, and 3
│   └── raw_interactions/   # Cached STRING database high-confidence edge lists (score ≥ 0.700)
├── notebooks/
│   └── tri_modal_network_analysis.ipynb  # End-to-end interactive Colab demonstration
├── src/
│   ├── __init__.py
│   ├── string_client.py     # Programmatic API querying for STRING database v12
│   ├── topology_engine.py   # NetworkX degree, betweenness centrality, and clustering
│   └── hub_visualizer.py    # cytoHubba-style ranked visualizations and SVG exports
├── results/
│   ├── figures/             # 600 DPI publication-grade figures
│   └── tables/              # Exported CSV topological metric tables (Table S2A-C)
├── environment.yml          # Pinned Conda environment
├── CITATION.cff             # Academic citation specification
└── README.md
```

---

## Quickstart (Google Colab)

Execute the end-to-end network pharmacology pipeline directly in your browser:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aakilkhanemon/Mpox-Systems-Pharmacology-Analysis/blob/main/notebooks/tri_modal_network_analysis.ipynb)

---

## Local Installation

```bash
git clone [https://github.com/aakilkhanemon/Mpox-Systems-Pharmacology-Analysis.git](https://github.com/aakilkhanemon/Mpox-Systems-Pharmacology-Analysis.git)
cd Mpox-Systems-Pharmacology-Analysis

# Create and activate virtual environment
conda env create -f environment.yml
conda activate mpox-network-pharm
```

### Reproducing Network Metrics & Hub Tables

Execute the complete analysis to recalculate topological metrics and regenerate Tables S2A–S2C:

```bash
python -m src.topology_engine \
  --targets data/targets/tri_modal_lead_targets.json \
  --confidence-score 700 \
  --out-dir results/tables/
```

### Generating cytoHubba Visualizations

Render the publication-ready, degree-ranked network graphs:

```bash
python -m src.hub_visualizer \
  --metrics-dir results/tables/ \
  --out-dir results/figures/ \
  --dpi 600
```

---

## Citation

```bibtex
@article{Emon2026MpoxTriModal,
  author = {Emon, Mohammed and Siddiquee, Noimul Hasan and Barman, Kripa and Haque, Md. Enamul},
  title = {System Pharmacology-Driven Tri-Modal Leads Discovery of Anti-Mpox Therapeutics: Integrating Quantum Mechanics, Molecular Dynamics, and Network Topology},
  journal = {ChemRxiv},
  year = {2026},
  doi = {10.26434/chemrxiv.15003736/v1},
  url = {[https://doi.org/10.26434/chemrxiv.15003736/v1](https://doi.org/10.26434/chemrxiv.15003736/v1)}
}
```
