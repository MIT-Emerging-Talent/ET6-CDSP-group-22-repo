# 📦 Welcome to The Express: A Collaborative Data Science Project on U.S. Retail Supply Chain Delays

![Your package is out for delivery meme](./4_data_analysis/images/delivery%20meme.jpg)

Welcome to **The Express**, a collaborative data science initiative developed to investigate the persistent issue of delivery delays in the U.S. retail supply chain. Combining real-world logistics data from Southern California and a systems thinking approach, this project aims to uncover the complex interdependencies among operational, environmental, and behavioral factors that contribute to delivery disruptions. Our analysis informs strategies to mitigate such delays and improve retail supply chain performance.

---

## 📘 Table of Contents

- [Project Overview](#project-overview)  
- [Problem Statement](#problem-statement)  
- [Research Questions](#research-questions)  
- [Dataset and Preparation](#dataset-and-preparation)  
- [Exploratory Analysis and Methodology](#exploratory-analysis-and-methodology)  
- [Findings](#findings)  
- [Limitations and Future Work](#limitations-and-future-work)  
- [Project Milestones](#project-milestones)  
- [Tech Stack](#tech-stack)  
- [Repository Structure](#repository-structure)  
- [Setup and Usage](#setup-and-usage)  
- [Team and Collaboration](#team-and-collaboration)  
- [License](#license)  
- [Acknowledgments](#acknowledgments)


---

## 🧭 Project Overview

Supply chain reliability has become critical for competitive success in retail, with rising consumer expectations for fast and reliable delivery. However, U.S. retailers continue to face delivery delays, especially during peak seasons or in metropolitan areas. Despite technological advancements such as real-time tracking and predictive routing, these delays persist. The Express investigates these inefficiencies through statistical and systems-based analysis to identify root causes and develop actionable insights.

---

## 📌 Problem Statement

The retail supply chain in the United States is experiencing increasingly complex and systemic delays, causing ripple effects across customer satisfaction, business revenue, and national logistics capacity. Our project centers on the Southern California region—a logistics hub with high volumes of freight movement via truck, rail, and sea. Through a data-driven approach, we aim to answer why delivery delays continue despite modernization and how data science can guide interventions.

---

## 🎯 Research Questions

**Primary Research Question:**
- What are the key operational, environmental, and behavioral factors that contribute to delivery delays in the U.S. retail supply chain, and how can they be mitigated using data science?

**Supporting Questions:**
- What impact do traffic congestion, port conditions, warehouse performance, and environmental factors have on delivery timing?
- Can we predict delivery delays based on real-time logistics and sensor data?
- How do seasonal surges and disruptive events (e.g., winter storms, labor strikes) affect last-mile delivery?
- Which features have the most significant influence when considered together?

---

## 🧮 Data Modelling and Preparation 

We used a dataset titled *Southern California Supply Chain Logistics Data* from Kaggle. It includes 32,066 records and 26 variables collected hourly between 2021 and 2024. The dataset represents operational data across multiple modes of transport (trucks, rail, drones), enriched with GPS, sensor, and warehouse data.

### Key Preparation Steps:
- Loaded and explored using pandas and Jupyter Notebooks
- Removed duplicate and irrelevant columns
- Validated column types, formats, and ranges
- Identified inconsistencies between documented schema and actual values (e.g., order status as floats rather than binary)

### Key Feature Categories:
- **Logistics**: Fuel usage, equipment availability, loading time  
- **Environmental**: Weather severity, port congestion, traffic conditions  
- **Operational**: Order fulfillment rate, lead time, supplier reliability  

### Target Variables:
- `delivery_time_deviation` (hours): Actual vs. estimated delivery time  
- `delay_probability` (float): Predicted likelihood of delay  
- `delay_risk_class` (categorical): Low, Moderate, High risk levels  

---

## 📊 Data Analysis and Methodology

### Phase I: Raw Dataset

We used Pearson, Spearman, and Kendall Tau correlation metrics to analyze relationships between 16 features and 3 delay indicators. All individual correlations were weak—none exceeded 0.012.

### Phase II: Corrected Dataset

After re-aligning variable definitions with documented expectations (e.g., binary flags, correct scales), we re-ran the analysis. This revealed stronger patterns through manual interaction analysis.

### Summary:

- Correlation matrices were mostly inconclusive.  
- Manual interaction analysis (e.g., high traffic + low inventory) showed higher predictive power.  
- We prioritized interpretability and did not use machine learning in this phase, but recommend ensemble models for future work.  

---

## 📈 Findings

- No single variable strongly correlates with delivery delay.  
- Port congestion repeatedly emerged as the most consistently relevant variable across models.  
- Compound risk factors (e.g., bad weather + driver fatigue or customs delays + low equipment availability) were more predictive of delivery time deviation than any single factor.  
- Heatmaps and multi-dimensional plots offered clearer insights than raw correlation.  
- These findings align with theories of cascading disruptions and ripple effects described in global supply chain literature.

> The strongest relationship we found was only 0.0118 between port congestion and delivery time deviation—extremely close to zero.

![Figure I: Three techniques outcome](./4_data_analysis/images/figure_3.png)

*Figure I: A heatmap that illustrates the correlation between the independent variables and the dependent.*

![Heatmap](./4_data_analysis/images/figure_5.jpeg)

---

## ⚠️ Limitations and Future Work

### Known Limitations:
- No temporal modeling—data is cross-sectional and cannot track evolving conditions  
- Sensor data contains inconsistencies (e.g., negative temperatures in Southern California)  
- No product categorization—treats perishable and durable goods equally  
- Lacks representation of rare but critical disruptions (e.g., strikes, earthquakes)  

### Future Work:
- Apply machine learning models (e.g., XGBoost, SHAP) to automatically detect nonlinear interactions  
- Incorporate time-series modeling and regional identifiers  
- Integrate external datasets on labor disruptions, weather anomalies, and economic policy shocks  
- Build a real-time risk dashboard for supply chain managers  

---

## 📆 Project Milestones

| Milestone | Description |
|----------|-------------|
| **0 - Cross-Cultural Collaboration** | Formed a global team and established shared norms, values, and tools using GitHub and structured documentation. |
| **1 - Problem Identification** | Scoped our research domain through literature review, data discovery, and systems thinking. |
| **2 - Data Collection** | Selected, cleaned, and documented a comprehensive dataset on Southern California logistics operations. |
| **3 - Data Analysis** | Conducted EDA, correlation analysis, and interaction modeling. |
| **4 - Communicating Results** | Designed visuals and messaging tailored to supply chain stakeholders. |
| **5 - Final Presentation** | Shared findings with MIT Emerging Talent faculty, peers, and partners. |

---

## 🧰 Tech Stack

- **Python**: `pandas`, `numpy`, `seaborn`, `matplotlib`  
- **Jupyter Notebooks**: for exploration, cleaning, and correlation analysis  
- **Tableau**: for dashboards and stakeholder visualizations  
- **Git + GitHub**: for collaboration, version control, and project coordination  

---

## 📂 Repository Structure

```plaintext
The-Express/
├── 0_domain_study/
├── 1_datasets/
├── 2_data_preparation/
├── 3_data_exploration/
├── 4_data_analysis/
├── 5_communication_strategy/
├── 6_final_presentation/
├── collaboration/
├── notes/
├── requirements.txt
└── README.md
```

## ⚙️ Setup and Usage

To run this project locally:

```bash
# Clone the repository
git clone https://github.com/MIT-Emerging-Talent/ET6-CDSP-group-22-repo.git
cd ET6-CDSP-group-22-repo

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate       # On macOS/Linux
# OR
venv\Scripts\activate          # On Windows

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter Notebook
jupyter notebook
```

## 👥 Proejct Team Members

This project was built by a global team of passionate learners as part of the **MIT Emerging Talent Program**.

- [Jawid Mohseni](https://github.com/JawidMohseni)  
- [Razan Ibrahim](https://github.com/Razan-O-Elobeid)  
- [Ismatova Rumiya](https://github.com/Ismatova-Rumiya)  
- [Alemayehu Desta](https://github.com/Alemayehu-Desta)  
- [Omnia Shawir](https://github.com/omniaNS)

---

## 📜 License

This project is licensed under the **MIT License**.  
See the [LICENSE](./LICENSE) file for full details.

---

## 🙏 Acknowledgments

We extend our sincere gratitude to the **MIT Emerging Talent Program** for providing the structure, mentorship, and global platform that made this collaboration possible.

Special thanks to:
- The instructors and mentors who guided us at every stage
- The open-source data community for making rich datasets publicly available

This project stands as a testament to cross-cultural teamwork, data-driven thinking, and the power of collective learning.



