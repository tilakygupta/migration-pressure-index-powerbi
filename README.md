# 🗺️ Migration Pressure Index — Indian States Dashboard
### Microsoft Elevate AICTE Internship | Power BI Capstone Project

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Data Source](https://img.shields.io/badge/Data-NDAP%20%7C%20Census%202011-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

---

## 📌 Project Overview

India has over **45.6 crore internal migrants** — 38% of the total population.
Between 2001 and 2011, the migrant population grew by **45%**, yet no unified
open-data dashboard existed combining push and pull factors to map migration
pressure at the state level.

This project builds the **first open-data Migration Pressure Index (MPI) Dashboard**
for all 30 Indian states using Microsoft Power BI and real government datasets
from NDAP (ndap.niti.gov.in).

---

## 🖥️ Dashboard Pages

| Page | Title | Description |
|------|-------|-------------|
| 1 | 🗺️ National Overview | Filled map colored by MPI score, 4 KPI cards, region & migration type slicers |
| 2 | 📤 Push Factors | Unemployment, poverty, wage, literacy charts — why people leave |
| 3 | 📥 Pull Factors | Urban GDP, infrastructure, in-migration charts — why migrants arrive |
| 4 | 🔀 Migration Flows | Source → Destination heatmap matrix + top corridor bar chart |
| 5 | 📈 Trend Analysis | 2001 vs 2011 MPI comparison + wage growth + key insight text box |

---

## 🧮 MPI Formula (DAX)

The Migration Pressure Index is a composite score (0–100) calculated using
Min-Max normalized indicators:
```
MPI = ROUND(
  (UnempNorm  × 0.25) +
  (PovNorm    × 0.20) +
  (LitNorm    × 0.15) +
  (WageNorm   × 0.20) +
  (DrNorm     × 0.10) +
  (InfrNorm   × 0.10)
) × 100, 0)
```

| Indicator | Weight | Source |
|-----------|--------|--------|
| Unemployment Rate | 25% | PLFS / CMIE |
| Rural Poverty Ratio | 20% | Planning Commission 2011 |
| Literacy Deficit (100 - Literacy) | 15% | Census 2011 |
| Wage Gap (inverse of wage) | 20% | CMIE Daily Wages |
| Drought Frequency | 10% | NDAP Agriculture |
| Infrastructure Deficit | 10% | NFHS-5 / NHM |

### MPI Categories

| Score | Category | Color |
|-------|----------|-------|
| ≥ 70 | 🔴 Critical | Red |
| 55–70 | 🟠 High | Orange |
| 40–55 | 🟡 Moderate | Yellow |
| 28–40 | 🟢 Low | Light Green |
| < 28 | 🟩 Minimal | Green |

---

## 📊 Key Findings

- 🔴 **Bihar** has the highest MPI of **82 (Critical)**
  — 74.2% out-migration, 16.4% unemployment, ₹250 daily wage
- 🟢 **Delhi** has the lowest MPI of **22 (Minimal)**
  — 68.4% in-migration, ₹650 daily wage, ₹1,98,400 urban GDP
- 🔀 **Largest corridor: UP → Delhi (57 Lakh migrants)**,
  Bihar → Delhi (47 Lakh)
- 💰 **Wage gap is the #1 migration driver**
  — Bihar ₹250 vs Delhi ₹650 = **2.6× difference**
- 📉 Despite MPI improving 2001–2011, migration **GREW +44.9%**
  — demonstrating the aspiration effect

---

## 🗂️ Dataset Files

| File | Description | Source |
|------|-------------|--------|
| `01_Migration_Pressure_Index.csv` | MPI scores + all indicators for 30 states | Compiled |
| `02_Migration_Flows.csv` | Source → Destination corridors (Lakhs) | Census 2011 D-Series |
| `03_Push_Factors.csv` | Unemployment, poverty, wages, literacy (2001 + 2011) | PLFS, BPL, Census |
| `04_Pull_Factors.csv` | Urban GDP, infrastructure, in-migration rates | NFHS-5, CMIE |
| `05_Migration_Reasons.csv` | Why people migrate (Employment 62%, Marriage 21%…) | Census D-4 |
| `06_Trend_2001_2011.csv` | MPI change over the decade | Compiled |

### Data Sources

- 📋 Census of India 2011 — D-Series Migration Tables — censusindia.gov.in
- 🏛️ NDAP, NITI Aayog — ndap.niti.gov.in
- 📊 Periodic Labour Force Survey (PLFS) 2020-21 — mospi.gov.in
- 🏥 National Family Health Survey NFHS-5 (2019-21) — rchiips.org/nfhs
- 💹 CMIE — State-wise Unemployment & Wage Data — cmie.com
- 📖 Economic Survey 2022-23 — Ministry of Finance

---

## 🏗️ Data Model (Star Schema)
```
                    ┌─────────────────┐
                    │  MigrationIndex │  ← Central Fact Table
                    │  (30 states)    │
                    └────────┬────────┘
           ┌─────────────────┼─────────────────┐
           │                 │                 │
    ┌──────┴──────┐   ┌──────┴──────┐   ┌──────┴──────┐
    │ PushFactors │   │ PullFactors │   │  TrendData  │
    └─────────────┘   └─────────────┘   └─────────────┘
           │                 │
    ┌──────┴──────┐   ┌──────┴──────┐
    │MigReasons   │   │MigFlows     │
    └─────────────┘   └─────────────┘
```

All tables linked via `State` column — Many-to-One relationships.

---

## ⚙️ How to Run

1. **Clone this repository**
```bash
   git clone https://github.com/tilakygupta/migration-pressure-index.git
```

2. **Open Power BI Desktop**
   - Download free at: powerbi.microsoft.com/desktop

3. **Load the 6 CSV files**
   - Home → Get Data → Text/CSV → load each file individually

4. **Open the .pbix file** (if included)
   - File → Open → select `Migration_Pressure_Index.pbix`

5. **Refresh data if needed**
   - Home → Refresh

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Microsoft Power BI Desktop | Dashboard design and visualization |
| Power Query | Data loading, cleaning, transformation |
| DAX | Calculated columns and dynamic measures |
| Star Schema | Data modeling with 6 interlinked tables |
| NDAP / Census 2011 | Primary data sources |

---

## 📁 Repository Structure
```
migration-pressure-index/
│
├── data/
│   ├── 01_Migration_Pressure_Index.csv
│   ├── 02_Migration_Flows.csv
│   ├── 03_Push_Factors.csv
│   ├── 04_Pull_Factors.csv
│   ├── 05_Migration_Reasons.csv
│   └── 06_Trend_2001_2011.csv
│
├── screenshots/
│   ├── page1_overview.png
│   ├── page2_push_factors.png
│   ├── page3_pull_factors.png
│   ├── page4_flows.png
│   └── page5_trends.png
│
├── Migration_Pressure_Index.pbix
├── Migration_Pressure_Index_Presentation.pptx
└── README.md
```

---

## 👤 Author

**[Tilak Yogesh Gupta]**
[Thakur College of Engineering & Technology] | [Masters of Computer Applications]
Microsoft Elevate AICTE Internship — Power BI Track

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)]([https://linkedin.com/in/yourprofile](https://www.linkedin.com/in/tilak-gupta-0121b6220/))

---

## 🙏 Acknowledgements

- **Mentors:** Vignesh Muthuvelan Sir & Karthiga Srinivasan Mam
- **Program:** Microsoft Elevate AICTE Internship
- **Supported by:** Microsoft, AICTE & Edunet Foundation

---

## 📄 License

This project is open source under the
[MIT License](LICENSE).
Data sourced from publicly available government datasets (NDAP, Census 2011).
