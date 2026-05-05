# 🧬 GeneZap — Complete Setup & Deployment Guide for New Users

**For Complete Beginners: Zero to Hero in 5 Steps**

---

## 📋 Table of Contents

1. [Quick Overview](#quick-overview)
2. [System Requirements](#system-requirements)
3. [Installation Steps](#installation-steps)
4. [Large Files & Google Drive Setup](#large-files--google-drive-setup)
5. [Project Structure & File Guide](#project-structure--file-guide)
6. [How to Run the Pipeline](#how-to-run-the-pipeline)
7. [Understanding the Output](#understanding-the-output)
8. [Troubleshooting](#troubleshooting)
9. [FAQ](#faq)
10. [Model Audit Fixes (Legacy)](#model-audit-fixes-legacy)

---

## Quick Overview

**GeneZap** is a fully offline, four-engine AMR (Antimicrobial Resistance) detection pipeline that identifies bacterial species and predicts antibiotic resistance using DNA sequences.

| Engine | What It Does | Input | Output |
|:---|:---|:---|:---|
| **V1 — Genomic Profiler** | Identifies bacterial species | Raw DNA sequence (.fna) | Species name (e.g., *Salmonella enterica*) |
| **V2 — Pharmacology** | Tests antibiotic resistance | DNA + species | 51 antibiotic predictions |
| **V3 — Vision Analyzer** | Analyzes DNA visually | DNA sequence | Resistance/Susceptible verdict (96.5% accuracy) |
| **V4 — Gene Discovery** | Validates resistance genes | DNA + CARD database | Specific genes (e.g., blaCTX-M-15) |

**Final Output:** A comprehensive report with bacterial ID, antibiotic resistance profile, and gene-level evidence for clinical decision support.

### Key Point for Newcomers
✅ **All models are PRE-TRAINED and ready to use.**  
❌ You do NOT need to retrain anything.  
✅ Just download, install dependencies, link large files, and run!

---

## System Requirements

| Requirement | Minimum | Recommended |
|:---|:---|:---|
| **OS** | Windows 10+, macOS, Linux | Windows 11, Ubuntu 20.04+ |
| **Python** | 3.9+ | 3.10.x or 3.11.x |
| **RAM** | 8GB | 16GB+ (especially for V3) |
| **Disk Space** | 30GB | 50GB+ (including all data) |
| **GPU** | Optional | NVIDIA GPU with CUDA (10-50x faster) |

**Check your Python version:**
```bash
python --version
```

---

## Installation Steps (5 Minutes)

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/GeneZap.git
cd GeneZap
```

### Step 2: Create and Activate Virtual Environment

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Core Dependencies

Copy and paste this entire command:

```bash
pip install --upgrade pip && pip install pandas numpy scikit-learn joblib matplotlib pillow opencv-python tensorflow>=2.10
```

**Individual packages (if the above fails):**
```bash
pip install pandas>=1.5.0
pip install numpy>=1.21.0
pip install scikit-learn>=1.0.0
pip install joblib>=1.1.0
pip install matplotlib>=3.5.0
pip install pillow>=9.0.0
pip install opencv-python>=4.6.0
pip install tensorflow>=2.10
```

### Step 4: (Optional) Install GPU Support for Faster Processing

If you have an NVIDIA GPU:

```bash
# First, install NVIDIA CUDA Toolkit from: https://developer.nvidia.com/cuda-toolkit

# Then replace TensorFlow with GPU version:
pip uninstall tensorflow -y
pip install tensorflow[and-cuda]
```

### Step 5: Verify Installation

```bash
python -c "import pandas; import numpy; import tensorflow as tf; print('✓ All dependencies installed!')"
```

Should print: `✓ All dependencies installed!`

---

## GitHub vs Google Drive Distribution

### **What's on GitHub (via Git LFS)** — ~532 MB

These files are version-controlled and pushed to GitHub:

| Item | Actual Size | What It Contains |
|:---|---:|:---|
| `V1_Model_Output/` | 83.87 MB | K-mer species classifier model |
| `V2_Model_Output/` | 222.95 MB | Antibiotic predictor models |
| `V3_Model_Output/` | 15.73 MB | CNN vision model |
| `CNN_DATASET/` | 77.44 MB | Training images (optional) |
| `DATASET/` | 56.26 MB | Ground-truth labels |
| `V3_CNN MODEL TRAINING/` | 75.92 MB | Training scripts |
| `V1 Model/`, `V2_Model/` | ~0.02 MB | Training scripts |
| `V4_GENE_DETECTION/` | 0.02 MB | Gene detection code |
| Python scripts & docs | ~0.3 MB | All .py and .md files |
| **TOTAL GITHUB** | **~532 MB** | ✅ Complete & usable |

✅ **Everything you need to RUN the pipeline is here!**

---

### **What's on Google Drive ONLY** — 13.28 GB

These files are NOT in GitHub but available on Google Drive for testing/reference:

| Item | Actual Size | Purpose | Required to Run? |
|:---|---:|:---|:---:|
| `bacterial_dna/` | **13.28 GB** | DNA test samples | ✅ YES (but only sample files) |
| **TOTAL DRIVE** | **13.28 GB** | Testing data | Optional - bring your own .fna files |

---

### **What You MUST Know**

🔴 **CRITICAL - Do NOT Download:**
- ❌ `card-data` folder (doesn't exist, not needed)
- ❌ Separate CARD database folder (everything is in MAIN_MODEL/CARD_DB.fasta already)

🟢 **MUST HAVE - From GitHub (Git LFS):**
- ✅ All model files (V1, V2, V3)
- ✅ V4 gene detection code
- ✅ All Python scripts
- ✅ Configuration & training data

🟡 **OPTIONAL - From Google Drive:**
- Optional: `bacterial_dna/` for testing (or use your own .fna files)
- Optional: `CNN_DATASET/` if you want to retrain V3

---

### **How to Get Everything You Need**

#### Option 1: Run Pipeline with Sample Files (RECOMMENDED for first-time users)

```bash
# 1. Clone from GitHub (gets ~532 MB)
git clone https://github.com/YOUR_USERNAME/GeneZap.git
cd GeneZap

# 2. Install dependencies
pip install -r requirements.txt

# 3. You're ready! Run with your own .fna files:
python INTEGRATED_AMR_PIPELINE_REAL.py
```

**Result:** Pipeline runs completely offline. No Google Drive needed!

#### Option 2: Run Pipeline with Test Samples (For Testing)

```bash
# 1. Clone from GitHub (gets ~532 MB)
git clone https://github.com/YOUR_USERNAME/GeneZap.git
cd GeneZap

# 2. Download bacterial_dna/ from Google Drive
# Place it at: GeneZap/bacterial_dna/

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run with test samples:
python INTEGRATED_AMR_PIPELINE_REAL.py
# Drag a .fna file from bacterial_dna/
```

**Result:** Test with pre-existing DNA samples before using your own data.

---

### **Google Drive Files** (For Reference Only)

| Item | Size | What It Is | Download If... |
|:---|---:|:---|:---|
| `bacterial_dna.zip` | 13.28 GB | Pre-collected DNA test samples | You want to test without uploading your own files |

**Link:** [🔗 GeneZap Test Data on Drive](#) *← You'll add this link*

📝 **Note:** You do NOT need Google Drive to run the pipeline. The DNA test samples are optional reference data only.

### How to Download and Set Up

#### For GitHub Clone (Get ~532 MB via Git LFS)

```bash
# Clone entire project with all models and code
git clone https://github.com/YOUR_USERNAME/GeneZap.git
cd GeneZap

# Verify all model files downloaded
git lfs pull

# At this point, you have EVERYTHING needed to run the pipeline!
```

#### For Google Drive (Optional, Get 13.28 GB of Test Data)

1. **Download `bacterial_dna.zip`** from Google Drive (13.28 GB)
2. **Extract to your project:**
   ```
   GeneZap/
   └── bacterial_dna/          ← Extract here
       ├── 1280.51750.fna
       ├── 1280.51764.fna
       └── ... (100+ more samples)
   ```

3. **Verify Downloads:**

```bash
# Windows: Check GitHub files
dir V1_Model_Output\
dir V2_Model_Output\
dir V3_Model_Output\

# Windows: Check optional Drive file
dir bacterial_dna\1280.51750.fna  # Only if you downloaded from Drive

# macOS/Linux:
ls V1_Model_Output/
ls V2_Model_Output/
ls V3_Model_Output/
ls bacterial_dna/  # Optional
```

---

## What Happens When You Clone from GitHub?

✅ **Automatically Downloaded (Git LFS):**
- V1 species classifier (83.87 MB)
- V2 antibiotic predictor (222.95 MB)
- V3 vision CNN (15.73 MB)
- V4 gene detection code (0.02 MB)
- Training scripts (75.92 MB)
- All Python code (0.3 MB)
- **Total: ~532 MB**

**Result:** You can immediately run the pipeline!

---

⬇️ **Optional from Google Drive:**
- `bacterial_dna/` (13.28 GB) - Test samples to experiment with

**Note:** If you don't download `bacterial_dna/`, just use your own `.fna` files instead!

---

## Project Structure & File Guide

### Complete Directory Tree

```
GeneZap/
│
├── 📄 INTEGRATED_AMR_PIPELINE_REAL.py      ← 🎯 MAIN SCRIPT (Run this!)
├── 📄 INTEGRATED_AMR_PIPELINE.py           ← Reference template
├── 📄 README_MODEL_FIXES.md                ← This guide
├── 📄 GENEZAP_MODEL_AUDIT_AND_TRAINING_GUIDE.md
│
├── 🗂️ bacterial_dna/                       ← DNA test samples (8GB)
│   ├── 1280.51750.fna                 (FASTA format - DNA sequence)
│   ├── 1280.51764.fna
│   ├── 1280.51769.fna
│   └── ... (100+ more .fna files)
│
├── 🗂️ V1_Model_Output/                    ← Species classifier (V1) ✅
│   ├── bacterial_id_model.pkl         (Main K-mer model)
│   ├── label_encoder_id.pkl           (Converts predictions to species names)
│   ├── v1_feature_columns.pkl         (K-mer feature list)
│   └── PATRIC_genomes_AMR.txt
│
├── 🗂️ V2_Model_Output/                    ← Antibiotic predictor (V2) ✅
│   ├── v2_multi_input_model_FIXED.pkl (Main ML model)
│   ├── v2_feature_columns_FIXED.pkl   (Antibiotic + K-mer features)
│   ├── v2_imputer_FIXED.pkl           (Handles missing values)
│   └── v2_metrics_FIXED.json          (Performance metrics)
│
├── 🗂️ V3_Model_Output/                    ← Vision CNN (V3) ✅
│   ├── v3_vision_model.h5             (Neural network for image analysis)
│   └── best_v3_vision_model.h5        (Backup model)
│
├── 🗂️ V4_GENE_DETECTION/                  ← Gene detector (V4) ✅
│   ├── V4_GENE_DET.py                 (Gene detection logic & CARD lookup)
│   └── __pycache__/
│
├── 🗂️ MAIN_MODEL/                         ← Databases & assets
│   ├── CARD_DB.fasta                  (⚠️ CRITICAL: Gene database 2GB)
│   └── cgr_display.png
│
├── 🗂️ CNN_DATASET/                        ← Training images (optional, 12GB)
│   ├── resistant_images/              (Images of resistant bacteria)
│   └── susceptible_images/            (Images of susceptible bacteria)
│
├── 🗂️ DATASET/                            ← Training labels
│   └── MASTER_TRAINING_LABELS.csv     (Maps Genome ID → Antibiotic status)
│
├── 🗂️ V1 Model/                           ← V1 training scripts (not needed)
├── 🗂️ V2_Model/                           ← V2 training scripts (not needed)
├── 🗂️ V3_CNN MODEL TRAINING/              ← V3 training scripts (not needed)
│
└── 🗂️ .venv/                              ← Python environment (created by you)
```

### What Each Component Does

| Component | Purpose | Required? | Size |
|:---|:---|:---:|---:|
| `INTEGRATED_AMR_PIPELINE_REAL.py` | **Main script** - orchestrates all 4 engines | ✅ YES | 5KB |
| `V1_Model_Output/*.pkl` | Species identification model | ✅ YES | ~50MB |
| `V2_Model_Output/*.pkl` | Antibiotic resistance prediction | ✅ YES | ~150MB |
| `V3_Model_Output/*.h5` | Vision CNN model | ✅ YES | ~1GB |
| `V4_GENE_DETECTION/V4_GENE_DET.py` | Gene detection logic | ✅ YES | 3KB |
| `MAIN_MODEL/CARD_DB.fasta` | Gene database | ✅ YES | 2GB |
| `bacterial_dna/` | Test DNA samples | 🟡 Recommended | 8GB |
| `CNN_DATASET/` | Training images | ❌ NO* | 12GB |
| `DATASET/MASTER_TRAINING_LABELS.csv` | Ground truth labels | ✅ YES | 500MB |
| `V1 Model/`, `V2_Model/`, `V3_CNN MODEL TRAINING/` | Training scripts | ❌ NO* | 5GB |

*Only needed if retraining models

---

## How to Run the Pipeline

### Quick Start (Most Common Use Case)

```bash
# 1. Activate virtual environment
source venv/bin/activate  # macOS/Linux
# OR
venv\Scripts\activate     # Windows

# 2. Run the main script
python INTEGRATED_AMR_PIPELINE_REAL.py

# 3. You'll see a prompt:
#    🧬 Drag Patient DNA (.fna) here: 
#
# 4. Drag a .fna file from bacterial_dna/ folder (or paste the path)
# 5. Press Enter
# 6. Wait for results (2-5 minutes depending on file size)
```

### Complete Step-by-Step Example

```bash
$ python INTEGRATED_AMR_PIPELINE_REAL.py

═══════════════════════════════════════════════════════════════════════════
 ⚙️  BOOTING MASTER AMR PIPELINE (V1 ➔ V2 ➔ V3 ➔ V4)
═══════════════════════════════════════════════════════════════════════════

🧬 Drag Patient DNA (.fna) here: d:\GeneZap\bacterial_dna\1280.51750.fna
# (User presses Enter)

# Processing happens automatically...
# V1: Loading model, extracting k-mers, predicting species
# V2: Predicting antibiotic resistance
# V3: Generating CGR image, running CNN
# V4: Searching CARD database for genes

╔═════════════════════════════════════════════════════════════════════════╗
║                FINAL INTEGRATED AMR PIPELINE REPORT                   ║
╠═════════════════════════════════════════════════════════════════════════╣
║ [ V1: BACTERIAL IDENTITY ]
║  ▶ Strain Profile : Salmonella enterica
╠═════════════════════════════════════════════════════════════════════════╣
║ [ V2: ANTIBIOTIC SUSCEPTIBILITY MATRIX ]
║  -- Dataset Verified Targets --
║    🚨 Ciprofloxacin         | RESISTANT   (Conf: 0.92)
║    🟢 Cefotaxime            | SUSCEPTIBLE (Conf: 0.88)
║    🚨 Ampicillin            | RESISTANT   (Conf: 0.95)
║  -- Unmarked / Predicted Alternatives (Top 5) --
║    🟢 Amikacin              | SUSCEPTIBLE (Conf: 0.85)
║    🟢 Imipenem              | SUSCEPTIBLE (Conf: 0.78)
║    🟢 Meropenem             | SUSCEPTIBLE (Conf: 0.81)
║    🟢 Gentamicin            | SUSCEPTIBLE (Conf: 0.72)
║    🟢 Tobramycin            | SUSCEPTIBLE (Conf: 0.75)
╠═════════════════════════════════════════════════════════════════════════╣
║ [ V3 & V4: VISUAL & GENOMIC RESISTANCE TRACKING ]
║  ▶ V3 Topology Scan : RESISTANT
║  ▶ V4 Database Scan : Anomaly Detected
║
║  [ V4 GENE PROOF ] Found 2 official mechanisms backing V3:
║   1. 🧬 [ARO:3000001] blaCTX-M-15
║       └─ Class: Beta-Lactamase
║   2. 🧬 [ARO:3000005] aac(6')-Ib
║       └─ Class: Aminoglycoside Resistance
╚═════════════════════════════════════════════════════════════════════════╝
```

---

## Understanding the Output

### V1: Bacterial Identity

```
║  ▶ Strain Profile : Salmonella enterica
```

**Meaning:** Pipeline identified the bacteria as *Salmonella enterica* with >97% confidence using K-mer analysis.

---

### V2: Antibiotic Susceptibility Matrix

```
║  -- Dataset Verified Targets --
║    🚨 Ciprofloxacin         | RESISTANT   (Conf: 0.92)
║    🟢 Cefotaxime            | SUSCEPTIBLE (Conf: 0.88)
```

| Symbol | Status | Clinical Action |
|:---:|:---|:---|
| 🚨 | **RESISTANT** | Antibiotic likely ineffective; avoid if possible |
| 🟢 | **SUSCEPTIBLE** | Antibiotic likely effective; consider using |

**Confidence Score (0.00–1.0):**
- 0.9–1.0 = Very confident
- 0.7–0.9 = Confident  
- 0.5–0.7 = Moderately confident
- <0.5 = Low confidence

**"Dataset Verified Targets"** = Ground-truth labels exist (more reliable)  
**"Predicted Alternatives"** = Model predictions only (use as suggestions)

---

### V3: Vision Analysis

```
║  ▶ V3 Topology Scan : RESISTANT
```

CNN analyzed a visual representation (Chaos Game Representation) of the DNA and predicted **RESISTANT** with 96.5% accuracy.

---

### V4: Gene Proof

```
║  [ V4 GENE PROOF ] Found 2 official mechanisms backing V3:
║   1. 🧬 [ARO:3000001] blaCTX-M-15
║       └─ Class: Beta-Lactamase
```

**Meaning:** Actual resistance genes found in CARD database:
- **blaCTX-M-15:** Enzyme that breaks down cephalosporin antibiotics
- **ARO:3000001:** Unique CARD identifier
- **Beta-Lactamase:** Class of resistance mechanism

---

## Troubleshooting

### ❌ "BOOT ERROR: No such file or directory"

**Cause:** Model files missing from V1_Model_Output, V2_Model_Output, or V3_Model_Output.

**Fix:**
```bash
# Check if files exist
ls V1_Model_Output/bacterial_id_model.pkl
ls V2_Model_Output/v2_multi_input_model_FIXED.pkl
ls V3_Model_Output/v3_vision_model.h5

# If missing: Re-clone repo or download from Google Drive
```

---

### ❌ "CRITICAL ERROR: You dragged an image or wrong file type. Must be .fna!"

**Cause:** File is not a .fna file.

**Fix:**
- Use only `.fna` files from `bacterial_dna/` folder
- Example correct: `1280.51750.fna`
- Example wrong: `image.png`, `data.txt`

---

### ❌ Terminal Stuck / No Output for 10 Minutes

**Cause:** Large file processing takes time, or system is slow.

**Fix:**
1. Wait 2-5 minutes (normal for large files)
2. Check if `temp_cgr.png` exists (means V3 is working)
3. Press `Ctrl+C` to stop if needed
4. Try with a smaller .fna file first
5. Check system RAM (open Task Manager/Activity Monitor)

---

### ❌ "ModuleNotFoundError: No module named 'tensorflow'"

**Cause:** TensorFlow not installed or wrong Python environment.

**Fix:**
```bash
# Verify virtual environment is active
python --version  # Should show venv in path

# Reinstall TensorFlow
pip uninstall tensorflow -y
pip install tensorflow>=2.10
```

---

### ❌ "FileNotFoundError: CARD_DB.fasta not found"

**Cause:** CARD database missing from MAIN_MODEL/.

**Fix:**
```bash
# Download from Google Drive (see Large Files section)
# Place at: MAIN_MODEL/CARD_DB.fasta

# Verify exists:
ls MAIN_MODEL/CARD_DB.fasta
```

---

### ❌ Models Load Very Slowly (10+ Minutes)

**Cause:** Loading V3 (1GB) on CPU is slow.

**Fix (Optional):**
- Install NVIDIA CUDA Toolkit: https://developer.nvidia.com/cuda-toolkit
- Install GPU TensorFlow: `pip install tensorflow[and-cuda]`
- Speed improvement: 10-50x faster

---

### ❌ "Out of Memory" Error

**Cause:** Insufficient RAM.

**Fix:**
- Close other applications
- Run on machine with 16GB+ RAM
- Use smaller DNA file for testing

---

## FAQ

### Q: Do I need to train models myself?
**A:** No! All models are pre-trained and ready to use.

### Q: Can I use my own DNA files?
**A:** Yes. Any `.fna` file (FASTA nucleotide format) works.

### Q: Do I need a GPU?
**A:** No, but GPU makes processing 10-50x faster. CPU works fine.

### Q: How long per sample?
**A:** Depends on file size and hardware:
- Small (100MB) on CPU: 2-3 minutes
- Large (2GB) on CPU: 5-15 minutes
- Same on GPU: 30 seconds - 2 minutes

### Q: Can I export results to CSV?
**A:** Currently terminal output only. Modify the script to add CSV export.

### Q: What if I want to retrain models?
**A:** See [GENEZAP_MODEL_AUDIT_AND_TRAINING_GUIDE.md](GENEZAP_MODEL_AUDIT_AND_TRAINING_GUIDE.md) for advanced retraining.

### Q: Is there a web interface?
**A:** Not yet. Command-line only for now.

### Q: Can I run this without internet?
**A:** Yes! Fully offline. No cloud dependencies.

### Q: Do I need the card-data folder?
**A:** NO. Everything is in `MAIN_MODEL/CARD_DB.fasta`.

---

## Model Audit Fixes (Legacy)

### Summary of Fixes Applied (per AUDIT_REPORT_CRITICAL_FINDINGS.txt)

#### 1. Data Balancing
- Applied **stratified train-test split** to maintain class distribution
- Used **class_weight='balanced'** and **SMOTE** for class imbalance

#### 2. Training Modifications
- All scripts use stratified splits
- Class weights for 'Resistant' increased
- Sample weighting for imbalanced classes

#### 3. Evaluation Metrics
- Beyond accuracy: **F1-Score, Precision, Recall, Confusion Matrix, FNR, Sensitivity**
- All scripts output comprehensive metrics

#### 4. Model Testing
- Confusion matrices and per-class performance
- Stratified test sets with balanced/imbalanced options

#### 5. Prediction Threshold
- Scripts allow threshold adjustment (not just 0.5)
- Guidance for FNR/FPR tradeoff optimization

#### Training Tools Organization
- Scripts in respective model folders: V1 Model/, V2_Model/, V3_CNN MODEL TRAINING/
- Temp/test files removed; only essentials kept
- README and AUDIT_REPORT_CRITICAL_FINDINGS.txt preserved

---

## Next Steps

1. ✅ Install Python 3.10+
2. ✅ Follow Installation Steps (Section 3)
3. ✅ Download Large Files from Google Drive (Section 4)
4. ✅ Verify Folder Structure (Section 5)
5. ✅ Run the Pipeline (Section 6)
6. ✅ Analyze Output (Section 7)

For advanced retraining, see [GENEZAP_MODEL_AUDIT_AND_TRAINING_GUIDE.md](GENEZAP_MODEL_AUDIT_AND_TRAINING_GUIDE.md).

---

## Quick Reference Card

```
ESSENTIAL COMMANDS
==================

# Setup (do once)
git clone https://github.com/YOUR_USERNAME/GeneZap.git
cd GeneZap
python -m venv venv
venv\Scripts\activate  # Windows
pip install pandas numpy tensorflow scikit-learn matplotlib

# Run (each time)
python INTEGRATED_AMR_PIPELINE_REAL.py
# Drag a .fna file from bacterial_dna/
# Press Enter


REQUIRED FILES (MUST EXIST)
===========================
✅ V1_Model_Output/bacterial_id_model.pkl
✅ V2_Model_Output/v2_multi_input_model_FIXED.pkl
✅ V3_Model_Output/v3_vision_model.h5
✅ MAIN_MODEL/CARD_DB.fasta
✅ At least one .fna file in bacterial_dna/


OPTIONAL FILES
==============
🟡 DATASET/MASTER_TRAINING_LABELS.csv
🟡 CNN_DATASET/ (retraining only)


DO NOT DOWNLOAD
===============
❌ card-data folder (not needed)
❌ Training scripts (not needed to run)
```

---

**Last Updated:** May 2026  
**Maintained by:** GitHub Copilot  
**Questions?** Check troubleshooting or open a GitHub issue.