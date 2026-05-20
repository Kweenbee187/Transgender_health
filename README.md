# 🧠 Transgender Healthcare Bias — India 4D Simulation

> A spatiotemporal bias and fairness analysis tool built with synthetic data, visualizing how healthcare access disparities affect transgender individuals across Indian states over time.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
![HTML](https://img.shields.io/badge/Built%20with-HTML%2FJS-orange)
![Data](https://img.shields.io/badge/Data-Synthetic%20Only-red)
![Individuals](https://img.shields.io/badge/N-800%20Individuals-purple)
![States](https://img.shields.io/badge/States-16-teal)

---

## 📌 Overview

This project is a fully self-contained interactive simulation that models **algorithmic bias in transgender healthcare prediction** across 16 Indian states. It explores how a model's prediction errors differ between high-access and low-access healthcare regions — and demonstrates what a fairness-aware model correction looks like in practice.

The simulation spans **4 dimensions**:

| Dimension | Description |
|-----------|-------------|
| **Space** | 16 Indian states mapped geographically |
| **Time** | 11 time steps (T = 0 to 10 years) |
| **Distribution** | Biomarker (Hct) distributions per group & state |
| **Model** | Biased baseline vs. fairness-aware model toggle |

> ⚠️ **All data in this project is entirely synthetic and generated algorithmically. It does not represent real individuals, real patients, or real clinical records.**

---

## ✨ Features

### 🗺️ India Map — Bias Intensity by State
An interactive choropleth-style bubble map showing Mean Absolute Error (MAE) per state. Bubble size and color encode bias intensity; hover for detailed per-state stats.

### 📈 MAE Over Time by ACI Level
Line chart tracking prediction error trajectories across High, Medium, and Low Access & Care Index (ACI) regions. Dashed lines show the biased baseline; solid lines show the fair model.

### 🕸️ 4D Knowledge Graph — State Biomarker Distribution
A force-directed graph where:
- **Node size** = MAE magnitude
- **Outer ring color** = ACI level (blue / orange / red)
- **Purple upper arc** = TF_On deviation from expected mean
- **Cyan lower arc** = TM_On deviation from expected mean
- **Red pulse ring** = TM at-risk population > 30%
- **Edge thickness** = biomarker similarity between states
- Nodes are **draggable**

### 📊 Population at Risk Bar Chart
Percentage of TM_On individuals with Hct > 48 (a synthetic risk threshold), broken down by ACI level at the selected time step.

### ⚖️ Biased vs. Fair Model Toggle
Switch between the **baseline model** (group mean prediction) and a **fairness-aware model** (weighted by inverse error) to see real-time reduction in disparity across all visualizations.

---

## 🧪 How It Works

### Synthetic Population
- **800 individuals** across 16 states (50 per state: 25 TF_On, 25 TM_On)
- Biomarker values drawn from seeded normal distributions
- Drift applied over time: TF_On values decrease slightly (−0.20/yr), TM_On values increase (+0.30/yr)
- Noise injected based on ACI level

### Access & Care Index (ACI)
Reflects healthcare infrastructure quality — higher noise is added for lower ACI states:

| ACI Level | States | Noise σ |
|-----------|--------|---------|
| **High** | Delhi, Maharashtra, Karnataka, Gujarat, Punjab | 1.5 |
| **Medium** | Tamil Nadu, Kerala, West Bengal, M.Pradesh, Telangana | 3.0 |
| **Low** | Bihar, Assam, Rajasthan, U.Pradesh, Odisha, Jharkhand | 6.0 |

### Bias Metric
```
error_i  = |actual_i − group_mean|
Bias     = max(MAE across states) − min(MAE across states)
```

### Fairness Mitigation
```
w_i         = 1 / (error_i + ε)
fair_pred   = Σ(w · actual) / Σ(w)
```
Individuals with higher errors receive greater weight, pulling the weighted mean closer to them and reducing per-state MAE disparity.

---

## 🚀 Usage

No installation required. This is a **single-file HTML application** with zero external dependencies beyond CDN-loaded libraries.

1. Clone or download the repository
2. Open `trans_healthcare_bias_india.html` in any modern browser
3. Use the **PLAY** button or time slider to animate across time steps
4. Toggle **BIASED ↔ FAIR** to compare model behavior
5. Hover nodes on the knowledge graph for detailed state stats
6. Drag nodes to rearrange the knowledge graph layout

```bash
git clone https://github.com/Kweenbee187/Transgender_health.git
cd Transgender_health
# Open trans_healthcare_bias_india.html in your browser
```

---

## 🛠️ Tech Stack

| Library | Purpose |
|---------|---------|
| [Plotly.js 2.26](https://plotly.com/javascript/) | Map, time series, bar charts |
| [D3.js v7](https://d3js.org/) | Force-directed knowledge graph |
| Vanilla JavaScript | Simulation engine, state management |
| HTML5 / CSS3 | UI, layout, animations |

---

## 📁 Repository Structure

```
Transgender_health/
├── trans_healthcare_bias_india.html   # Main simulation (single file, self-contained)
├── LICENSE                            # Apache 2.0
└── README.md                          # This file
```

---

## ⚖️ License

Copyright © 2026 **Kweenbee187**

Licensed under the [Apache License, Version 2.0](./LICENSE). You may use, reproduce, and distribute this work in accordance with the license terms.

---

## 👤 Author

**Kweenbee187**

---

*This simulation is intended for educational and research visualization purposes only. All data is synthetic.*
