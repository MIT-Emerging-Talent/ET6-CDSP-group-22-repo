# Data Analysis

## Technical Description

### 1. Objective

The goal of this analysis is to explore and understand the factors associated
with delivery delays in logistics and supply chain operations. We aim to identify
which operational features are most correlated with delivery delay, using the
features and target variables available in our dataset.

Our analysis focused on descriptive analytics, specifically correlation analysis,
to measure the strength and direction of relationships between features and three
key delay indicators:

- `delay_probability`
- `delivery_time_deviation`
- `eta_variation_hours`

---

### 2. Methodology

#### 2.1 Why Correlation Analysis?

- Directly addresses factor identification research question
- Established method in supply chain research
- Creates foundation for advanced analytics

#### 2.2 Handling Inconsistencies

While inspecting the dataset, we encountered mismatches between the dataset
description and actual data content:

- Features `order_fulfillment_status`, `cargo_condition_status`,
`handling_equipment_availability`, described as binary (0 or 1), contained float
values between 0 and 1.
- Feature `historical_demand`, described to be in units, contained float values
100 and 10k.

To understand the impact of this inconsistency, we split the correlation analysis
into two phases:

#### 2.3 Dual-Phase Correlation Analysis

#### Phase 1

We used the dataset as-is and performed three correlation analysis techniques
because different mathematical approaches detect different types of
relationships in the same data.

- **Techniques Used:**

  - Pearson's correlation `scipy.stats.pearsonr()`:
    - Measures linear relationships between two continuous variables.
    - Assumes data is normally distributed and relationships follow straight-line
patterns.
    - Coefficient ranges from -1 (perfect negative linear relationship) to +1
(perfect positive linear relationship).
  - Spearman's rank correlation `scipy.stats.spearmanr()`:
    - Measures monotonic relationships by converting values to ranks first, then
applying Pearson correlation to the ranks.
    - Detects consistent directional patterns that may be curved (non-linear) but
still consistently increasing or decreasing.
  - Kendall's Tau Correlation `scipy.stats.kendalltau()`:
    - Measures ordinal association by comparing how often pairs of observations
  agree in their ranking order.
    - More robust to outliers and better at detecting threshold effects where
  relationships change at certain values.

- **Phase 1 Findings:**

  - All correlation coefficients across all three techniques were very weak (< 0.1).

  - **Strongest Correlations by Technique for the Unmodified Data:**
  
    Delay Probability:

    - Pearson: port_congestion_level (+0.0090)
    - Spearman: route_risk_level (-0.0069)
    - Kendall: route_risk_level (-0.0046)

    Delivery Time Deviation:

    - Pearson: port_congestion_level (+0.0106)
    - Spearman: port_congestion_level (+0.0118)
    - Kendall: port_congestion_level (+0.0079)

    ETA Variation Hours:

    - Pearson: supplier_reliability_score (+0.0079)
    - Spearman: lead_time_days (-0.0087)
    - Kendall: lead_time_days (-0.0058)

#### Phase 2

To assess whether data quality issues contributed to the weak correlations
observed in Phase 1, we conducted a second analysis using data modified to
adhere to the original dataset description.

- **Data Modifications Applied:**

  - Binary Variable Correction: `order_fulfillment_status`, `cargo_condition_status`,
  `handling_equipment_availability`: Converted continuous float values [0.0, 1.0]
  to discrete binary values {0, 1} using threshold-based classification (values ≥
  0.5 → 1, values < 0.5 → 0)

  - Unit Standardization: `historical_demand`: Applied consistent unit interpretation
  and scaling to resolve

- **Phase 2 Findings:**

  - Correlation coefficients remained weak (< 0.1) even after data corrections,
indicating that measurement inconsistencies were not the primary cause of weak relationships.

  - **Strongest Correlations by Technique for the Modified Data:**
  
    Delay Probability:

    - Pearson: port_congestion_level (+0.0089)
    - Spearman: route_risk_level (-0.0064)
    - Kendall: route_risk_level (-0.0044)

    Delivery Time Deviation:

    - Pearson: port_congestion_level (+0.0106)
    - Spearman: port_congestion_level (+0.0118)
    - Kendall: port_congestion_level (+0.0079)

    ETA Variation Hours:

    - Pearson: supplier_reliability_score (+0.0078)
    - Spearman: lead_time_days (-0.0085)
    - Kendall: lead_time_days (-0.0057)

#### 2.4 Interaction Effects Analysis

Given the universally weak individual correlations observed in both phases, we
conducted additional analysis to test whether **combinations of operational factors**
demonstrate stronger relationships with delivery delays than individual factors alone.

- **Interaction Features Created:**
  - `traffic_x_weather`: Traffic congestion × Weather severity
  - `port_x_customs`: Port congestion × Customs clearance time  
  - `route_x_driver`: Route risk × Driver behavior score

- **Method:** Applied Pearson correlation analysis to interaction features vs.
delay indicators

- **Findings:** Interaction correlations remained weak (< 0.1), showing no
substantial improvement over individual factors.

---

### 3. Results Summary

---

### 4. Possible Flaws

---

### 5. Possible Alternative Approaches

---

### 6. Replication and Files

---

### 7. Conclusion

---
