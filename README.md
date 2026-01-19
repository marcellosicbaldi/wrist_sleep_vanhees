# Sleep/Wake Detection from Accelerometry (VH2015) — Multi-dataset Evaluation

A practical, reproducible evaluation of the **Van Hees 2015 (VH2015)** open-source sleep/wake algorithm across **multiple datasets** and **sensor locations** (wrist, lower back, thigh), using **polysomnography (PSG)** as reference.

---

## ✨ Highlights

- 🌙 Evaluates **VH2015** sleep/wake scoring on raw triaxial accelerometry  
- 🧩 **4 public datasets**, **188 participants**, heterogeneous devices & settings  
- 📍 Beyond the wrist: includes **lower back** and **thigh** placements  
- 📊 Standard sleep-tracker reporting: epoch metrics + sleep-summary agreement  

---

## 🔍 What this repo is about

Wearable-based sleep is often inferred from movement. VH2015 is a widely used, **device-agnostic** and **fully open-source** approach that operates directly on raw accelerometer data (no proprietary “activity counts”).

This repository supports an evaluation of how well VH2015:
- detects **sleep vs wake** (epoch-by-epoch), and
- estimates sleep summaries (e.g., **TST**, **WASO**, **SE**)  
across **different cohorts**, **devices**, and **body locations**. :contentReference[oaicite:1]{index=1}

---

## 🧪 Datasets (public)

The study uses four publicly available datasets with simultaneous PSG + accelerometry:

| Dataset | n | Location(s) | Device |
|---|---:|---|---|
| NewcastlePSG | 28 | Wrist | GENEActiv |
| AppleWatch | 31 | Wrist | Apple Watch Series 3 |
| DREAMT | 100 | Wrist | Empatica E4 |
| DualSleep | 29 | Lower back + Thigh | Axivity AX3 |

Total: **188 participants** across lab/home and healthy/clinical cohorts. :contentReference[oaicite:2]{index=2}

---

## 🧠 Algorithm

- **VH2015** as implemented in **GGIR (R package)**  
- Operates on **raw triaxial acceleration**  
- Produces sleep/wake at **5-second resolution** (then aligned to PSG epochs) :contentReference[oaicite:3]{index=3}

---

## 🧾 Reference standard (PSG)

- PSG sleep stages are scored by trained experts in **30-second epochs** (AASM-based scoring in the source datasets).
- We use the released annotations as-is (no rescoring). :contentReference[oaicite:4]{index=4}

To align resolutions:
- VH2015 5s output → resampled to 30s via **majority voting**. :contentReference[oaicite:5]{index=5}

---

## 📊 Evaluation (high-level)

This repo reports:
- **Epoch-by-epoch** metrics (e.g., sensitivity, specificity, PABAK)
- **Sleep summary agreement** for common outcomes (TST, WASO, SE) using Bland–Altman-style discrepancy analysis
- Exploratory stratifications (e.g., healthy vs sleep-disorder groups where available) :contentReference[oaicite:6]{index=6}

---

## ✅ Key takeaways (headline)

- VH2015 shows **high sensitivity** for sleep detection across datasets and locations, but **lower specificity** for wake (quiet wake is hard to detect from motion alone). :contentReference[oaicite:7]{index=7}
- Performance is **broadly comparable across wrist, lower back, and thigh**, suggesting VH2015 can support studies that already place sensors for mobility assessment. :contentReference[oaicite:8]{index=8}
- Results show **large inter-individual variability**: some subjects are tracked very well, others poorly — important for individual-level use cases. :contentReference[oaicite:9]{index=9}

---

## 📁 Repository structure

```text
.
├─ data/                      # dataset pointers / download notes (no raw PSG here)
├─ src/
│  ├─ preprocessing/          # resampling, alignment, epoching
│  ├─ vh2015/                 # GGIR wrappers / configuration
│  ├─ evaluation/             # epoch metrics + discrepancy analysis
│  └─ utils/
├─ scripts/
│  ├─ run_vh2015_pipeline.*
│  ├─ align_with_psg.*
│  ├─ compute_metrics.*
│  └─ make_figures.*
├─ notebooks/                 # optional exploration
└─ results/                   # generated outputs (usually gitignored)
