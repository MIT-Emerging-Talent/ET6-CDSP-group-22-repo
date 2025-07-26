# 📦 The Express: A Collaborative Data Science Project on U.S. Retail Supply Chain Delays

**The Express** is a collaborative data science project focused on identifying the root causes of delivery delays in the U.S. retail supply chain. Using a systems thinking lens and real-world logistics data from Southern California, we explore how multiple operational and environmental factors interact to cause disruptions—and what can be done to prevent them.

---

## 📘 Table of Contents
1. [Project Overview](#project-overview)  
2. [Problem Statement](#problem-statement)  
3. [Research Questions](#research-questions)  
4. [Dataset & Preparation](#dataset--preparation)  
5. [Exploratory Analysis & Methodology](#exploratory-analysis--methodology)  
6. [Findings](#findings)  
7. [Limitations & Future Work](#limitations--future-work)  
8. [Project Milestones](#project-milestones)  
9. [Tech Stack](#tech-stack)  
10. [Repository Structure](#repository-structure)  
11. [Setup & Usage](#setup--usage)  
12. [Team & Collaboration](#team--collaboration)  
13. [License](#license)  
14. [Acknowledgments](#acknowledgments)

---

## 🧭 Project Overview

In an increasingly digital and fast-paced economy, delivery reliability is no longer a luxury—it’s a consumer expectation. Yet delays remain widespread, especially during peak seasons or in high-traffic urban areas. Our project uses data science techniques to analyze these challenges, identify patterns, and propose mitigation strategies through correlation analysis and interaction-based reasoning.

---

## 📌 Problem Statement

The U.S. retail supply chain suffers from widespread delivery delays, despite technological advances. These delays cost businesses money, hurt customer satisfaction, and reveal a fragile and poorly coordinated logistics system. Our goal is to identify the key causes of these delays and determine how predictive and descriptive analytics can support operational decision-making.

We focused on Southern California due to its complex logistics network, port activity, and high-volume retail delivery activity.

---

## 🎯 Research Questions

**Main Research Question:**
- What are the key factors contributing to delivery delays in the retail supply chain, and how can they be mitigated using data-driven methods?

**Supporting Questions:**
- How do congestion, weather, or warehouse conditions influence delays?
- Can we predict delays using machine learning or statistical tools?
- How do events like holidays or extreme weather impact last-mile delivery?
- Are some risk factors more dangerous in combination than alone?

---

## 🧮 Dataset & Preparation

**Source**: Kaggle – Southern California Logistics Dataset (2021–2024)  
**Rows**: 32,066  
**Columns**: 26  
**Scope**: Trucks, rail, drones; GPS logs, IoT sensors, warehouse data

### Data Cleaning Steps
- Loaded with `pandas`; no source modification
- Removed irrelevant columns
- Verified no missing or duplicate records
- Identified inconsistencies in value ranges vs. documented schema

### Feature Groups
- **Logistics**: fuel use, handling time, equipment availability
- **Environmental**: traffic level, weather severity, port congestion
- **Operational**: lead time, order fulfillment, customs clearance

### Target Variables
- `delivery_time_deviation`: hours early/late
- `delay_probability`: delay likelihood (0–1)
- `delay_risk_class`: risk bucket (Low, Moderate, High)

---

## 📊 Exploratory Analysis & Methodology

### Phase I: Raw Dataset
- Used Pearson, Spearman, and Kendall Tau to identify correlates
- Found extremely weak correlations (max ~0.01)

### Phase II: Corrected Dataset
- Re-coded features based on documentation
- Performed interaction analysis manually
- Found that **compound risks** (e.g., weather + port congestion) are more predictive than any single feature

### Additional Analysis
- Visual heatmaps and interaction plots helped uncover subtle multivariate patterns
- Decided against machine learning to prioritize interpretability, though ML is proposed for future work

---

## 📈 Findings

- **No strong single predictors** of delay  
- **Port congestion** was consistently among the top (albeit weak) indicators  
- **Compounded risks** (e.g., high traffic + low equipment availability) were the strongest contributors to delay  
- Traditional correlation methods are insufficient alone—interaction analysis is more informative  
- Literature supports a ripple effect in supply chains (Jusda 2023, IMF 2022, MIT SCM 2023)

![Figure III: Interaction Heatmap of Top Risk Factors](./4_data_analysis/images/figure3_interaction_heatmap.png)

*Figure III: A visual representation of how compound factors (e.g., high port congestion + low inventory) lead to greater delivery time deviations.*

---

## ⚠️ Limitations & Future Work

- Data is cross-sectional—not time-series
- Some sensors recorded implausible values (e.g., –10°C in California)
- No product-type differentiation (perishable vs. non-perishable)
- Missing high-impact disruption records (e.g., labor strikes, natural disasters)

**Next Steps**:
- Use machine learning (e.g., XGBoost + SHAP) for deeper pattern detection
- Incorporate time-series and geospatial context
- Build risk dashboards for supply chain managers

---

## 📆 Project Milestones

| Milestone | Description |
|----------|-------------|
| **0 - Cross-Cultural Collaboration** | Established norms, set up GitHub, and coordinated across diverse backgrounds. |
| **1 - Problem Identification** | Researched domain and scoped our problem within retail logistics. |
| **2 - Data Collection** | Selected and cleaned Southern California logistics data. |
| **3 - Data Analysis** | Ran statistical and interaction-based analyses. |
| **4 - Communicating Results** | Created visualizations and translated findings for stakeholders. |
| **5 - Final Presentation** | Presented insights to MIT Emerging Talent cohort and partners. |

---

## 🧰 Tech Stack

- **Python**: `pandas`, `numpy`, `matplotlib`, `seaborn`
- **Jupyter Notebooks**: for EDA and modeling
- **Tableau**: for stakeholder dashboards
- **GitHub**: for version control and collaboration

---

## 🗂️ Repository Structure

```plaintext
The-Express/
├── 0_domain_study/                 # Background research and brainstorming
│   ├── README.md
│   ├── brainstorming.md
│   └── guide.md
│
├── 1_datasets/                     # Raw, cleaned, and unused datasets
│   ├── cleaned_and_processed_data/
│   ├── raw_data/
│   ├── unused_data_set_1/
│   ├── README.md
│   └── guide.md
│
├── 2_data_preparation/            # Data loading and cleaning scripts
│   ├── clean_dataset.py
│   ├── README.md
│   └── guide.md
│
├── 3_data_exploration/            # EDA notebooks and summaries
│   ├── eda_supply_chain.ipynb
│   ├── README.md
│   └── guide.md
│
├── 4_data_analysis/               # Modeling and correlation summaries
│   ├── images/
│   ├── notebooks/
│   ├── summary_of_analysis_of_cdsp.md
│   ├── README.md
│   └── guide.md
│
├── 5_communication_strategy/      # Messaging, storytelling, stakeholder focus
│   ├── README.md
│   └── guide.md
│
├── 6_final_presentation/          # Public-facing presentation files
│   ├── README.md
│   └── guide.md
│
├── collaboration/                 # Team norms and retrospective notes
│   ├── guide/
│   ├── retrospectives/
│   ├── communication.md
│   ├── constraints.md
│   ├── learning_goals.md
│   └── README.md
│
├── notes/                         # Miscellaneous team notes
│   └── README.md
│
├── requirements.txt               # Python dependencies
└── README.md                      # Main documentation
⚙️ Setup & Usage
Clone the repository:

bash
Copy
Edit
git clone https://github.com/YOUR_ORG/The-Express.git
cd The-Express
Create and activate a virtual environment:

bash
Copy
Edit
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate
pip install -r requirements.txt
Launch notebooks:

bash
Copy
Edit
jupyter notebook
👥 Team & Collaboration
Name	GitHub
Jawid Mohseni	@JawidMohseni
Razan Ibrahim	@Razan-O-Elobeid
Rumiya	@Ismatova-Rumiya
Alemayehu Desta	@Alemayehu-Desta
Omnia	@omniaNS

See collaboration/ for team norms and retrospective documentation.

📄 License
This project is licensed under the MIT License. See LICENSE for full terms.

🙏 Acknowledgments
We thank the MIT Emerging Talent Program, our mentors, and supply chain stakeholders for their guidance. Special thanks to open-source communities and platforms like Kaggle for making impactful data accessible.
