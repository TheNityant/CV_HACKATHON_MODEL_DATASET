# 🧬 GeneZap: Integrated AMR Pipeline

Welcome to **GeneZap**, a next-generation, fully offline clinical decision support tool for rapid bacterial pathogen identification and antimicrobial resistance (AMR) profiling. It processes raw genetic sequencer files (FASTA/FNA) to deliver actionable, high-confidence recommendations for clinicians, while ensuring patient data never leaves the local environment.

## 🚀 Quick Overview

GeneZap combines four specialized AI engines for robust, multi-modal analysis:

| Engine | Modality | Output |
| :--- | :---: | :--- |
| **V1 — Genomic Profiler** | 📊 NLP/Text | Species ID via K-mer indexing (>97% confidence) |
| **V2 — Pharmacology** | 💊 ML | Resistance/susceptibility for 51 antibiotics |
| **V3 — Vision Analyzer** | 🖼️ CV | CGR image + CNN for visual anomaly detection |
| **V4 — Gene Discovery** | 🔬 DB Alignment | CARD database gene validation (e.g., NDM-1) |

## 📚 Documentation & Guides

For detailed instructions, deployment setups, and model audit records, please refer to the following comprehensive guides:

- [**GeneZap — Complete Setup & Deployment Guide for New Users** (`README_MODEL_FIXES.md`)](./README_MODEL_FIXES.md)
  *Includes full system requirements, step-by-step installation instructions, and large file handling.*
- [**Model Audit, Safety, and Training Guide** (`GENEZAP_MODEL_AUDIT_AND_TRAINING_GUIDE.md`)](./GENEZAP_MODEL_AUDIT_AND_TRAINING_GUIDE.md)
  *Details on clinical context, pipeline logic, security features, and model safety practices.*

## ⚙️ Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/TheNityant/CV_HACKATHON_MODEL_DATASET.git
   cd CV_HACKATHON_MODEL_DATASET
   ```
2. **Set up virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # macOS/Linux
   venv\Scripts\activate     # Windows
   ```
3. **Install dependencies**
   ```bash
   pip install --upgrade pip
   pip install pandas numpy scikit-learn joblib matplotlib pillow opencv-python tensorflow>=2.10
   ```

## 💻 Usage

To run the full integrated pipeline on a `.fna` sample:

```bash
python INTEGRATED_AMR_PIPELINE_REAL.py
```

### Example Output

```
=== INTEGRATED AMR PIPELINE REPORT ===
V1 Bacteria: Salmonella enterica
V3 Bacteria: Salmonella enterica
Bacteria ID Match: True
V3 Gene: blaCTX-M-15
Gene Verified by V4 (CARD): True
Recommended Antibiotics: ciprofloxacin, cefotaxime
```

## 🔒 Security & Privacy

GeneZap runs **100% offline**. There are no external API calls, cloud dependencies, or telemetry, making it ideal for clinical environments requiring strict data privacy compliance (e.g., HIPAA).

