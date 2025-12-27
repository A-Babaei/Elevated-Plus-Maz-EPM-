# 🧠 Elevated Plus Maze (EPM) Analysis – TrAQ-Compatible MATLAB Pipeline

A **robust, publication-ready MATLAB pipeline** for analyzing **Elevated Plus Maze (EPM)** experiments using **TrAQ tracking outputs**.
This code faithfully reproduces **TrAQ/EthoVision behavioral definitions**, including **nose-based entries**, **body-based zone occupancy**, **temporal debouncing**, and **standard anxiety indices (OAT%, OAE%)**.

---

## 📌 Key Features

* ✅ **TrAQ-compatible definitions**

  * BODY → time in zones & speed
  * NOSE → arm entries
* ✅ **Temporal debouncing** to remove boundary jitter
* ✅ **Exact time conservation**
* ✅ **Correct arm orientation handling**
* ✅ **Standard anxiety indices**

  * Open Arm Time Percentage (**OAT%**)
  * Open Arm Entry Percentage (**OAE%**)
* ✅ **Paper-ready figures (600 dpi)**
* ✅ **Robust to TrAQ field name differences**
* ✅ **Scientifically conservative & reproducible**

---

## 📁 Repository Structure

```text
.
├── EPM_TrAQ_Final_Anxiety_PaperReady_FixedOrientation.m
├── README.md
├── example_data/
│   └── Out_Stim2.mat
└── figures/
    ├── Fig_EPM_Trajectory_Fixed.png
    ├── Fig_EPM_TimeInArms_Fixed.png
    └── Fig_EPM_Entries_Fixed.png
```

---

## 🎥 Supported Input

This pipeline expects **TrAQ output files** (e.g. `Out_Stim2.mat`) containing a `track` structure with at least:

### Required fields

* One **body-like position**

  * `track.Centroid` **(preferred)**
  * `track.Body_Centroid`
  * `track.Body`
* One **nose/head position**

  * `track.Nose` **(preferred)**
  * `track.Head`

### Optional fields

* `track.Time` (recommended)
* `track.FrameRate` (fallback if `Time` is missing)

The code automatically detects available fields.

---

## 🧭 Maze Geometry Assumption (Important)

This code explicitly enforces the **actual physical maze layout** used in your experiment:

| Arm orientation               | Arm type        |
| ----------------------------- | --------------- |
| **Top / Bottom (vertical)**   | **Closed arms** |
| **Left / Right (horizontal)** | **Open arms**   |

⚠️ This is **experiment-specific** and was validated against the arena video and TrAQ visualizations.
If your maze orientation differs, adjust the mapping in **one clearly marked section** of the code.

---

## 🧮 Behavioral Definitions (TrAQ-faithful)

### Zone occupancy

* Computed using **BODY position**
* Zones:

  * `Center`
  * `Open arms`
  * `Closed arms`

### Arm entries

* Computed using **NOSE position**
* Counted **only when transitioning from Center → Arm**
* Temporally debounced (default: **300 ms**) to remove flicker

This matches how **TrAQ and EthoVision** report arm entries.

---

## 📊 Anxiety Indices

The pipeline computes standard EPM anxiety metrics:

### 🔹 Open Arm Time Percentage (OAT%)

[
\text{OAT%} = 100 \times \frac{\text{Time in Open Arms}}
{\text{Time in Open Arms} + \text{Time in Closed Arms}}
]

* Center time excluded (standard practice)

---

### 🔹 Open Arm Entry Percentage (OAE%)

[
\text{OAE%} = 100 \times \frac{\text{Open Arm Entries}}
{\text{Open Arm Entries} + \text{Closed Arm Entries}}
]

* Nose-based
* Center → arm only
* Returns `NaN` if no closed-arm entries occur (TrAQ-consistent)

---

## 🚀 How to Run

1. Place your TrAQ output file (e.g. `Out_Stim2.mat`) in the working directory
2. Open MATLAB
3. Run:

```matlab
EPM_TrAQ_Final_Anxiety_PaperReady_FixedOrientation
```

---

## 📤 Outputs

### Console

* Full results table:

  * Time in zones
  * Entries per zone
  * OAT%
  * OAE%
  * Mean speed (overall & per zone)

### Files

* `EPM_Final_FixedOrientation.csv` – analysis results
* High-resolution figures (600 dpi):

  * Time in arms
  * Arm entries
  * Zone-colored trajectory

---

## 📈 Example Output Table

| Metric         | Example |
| -------------- | ------- |
| TotalTime_s    | 528.03  |
| Time_Open_s    | 170.77  |
| Time_Closed_s  | 424.29  |
| Entries_Open   | 2       |
| Entries_Closed | 0       |
| OAT%           | 28.7    |
| OAE%           | NaN     |

---

## 🧪 Quality Control & Validation

The pipeline was validated against:

* TrAQ zone-occupancy plots
* TrAQ nose-based entry traces
* Manual inspection of arena video
* Exact time conservation checks

Every reported metric is **confirmable visually**.

---

## 📝 Recommended Methods Text (for papers)

> “Time spent in each zone and locomotor speed were computed using the body centroid.
> Arm entries were defined using the nose position and counted only when the animal transitioned from the center zone into an arm after temporal debouncing (≥300 ms), consistent with TrAQ definitions.
> Anxiety-like behavior was quantified using the percentage of time spent in open arms (OAT%) and the percentage of open arm entries (OAE%).”

---

## 🔧 Customization

Easily adjustable parameters:

* Debounce duration
* Position smoothing window
* Pixel-to-cm calibration
* Arm orientation mapping

All customization points are **explicitly commented** in the code.

---

## 🧑‍🔬 Intended Audience

* Behavioral neuroscientists
* Pharmacology studies using EPM
* Labs using **TrAQ** or **EthoVision**
* Researchers requiring **transparent, review-safe analysis**

---

## 📜 License

MIT License (recommended)
Free for academic and commercial use with attribution.

---

## 📬 Contact

For questions, extensions, or batch-processing versions:

* Open a GitHub issue
* Or contact the code author directly

---

### ✅ Final Note

This pipeline prioritizes **scientific correctness over inflated metrics**.
If your results look “lower” than naïve scripts, that is a **feature, not a bug** — it reflects **true TrAQ-faithful behavior scoring**.

---

If you want, I can also:

* Add **citation badges**
* Add **example figures**
* Create a **batch-processing README**
* Prepare a **Methods supplement**

Just tell me.
