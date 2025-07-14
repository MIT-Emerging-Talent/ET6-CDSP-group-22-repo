# Data Analysis

## Technical Description

### 1. Objective

The goal of this analysis is to explore and understand the factors contributing
to delivery delays in logistics and supply chain operations. We aim to identify
which operational features are most correlated with delivery delay, using the
features and target variables available in our dataset.

Our analysis focused on descriptive analytics, specifically correlation analysis,
to measure the strength and direction of relationships between features and two
key delay indicators:

- `delay_probability`
- `delivery_time_deviation`

---

### 2. Methodology

#### 2.1 Why Correlation Analysis?

- Directly addresses factor identification research question
- Established method in supply chain research
- Creates foundation for advanced analytics

#### 2.2 Handling Inconsistencies

While inspecting our dataset, we encountered mismatches between the dataset
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

We used the dataset as-is, working with all numeric features including float-type
values. We performed three correlation analysis techniques because different
mathematical approaches detect different types of relationships in the same data.

- **Techniques Used:**

  - Pearson's correlation:
    - Measures linear relationships between two continuous variables.
    - Assumes data is normally distributed and relationships follow straight-line
patterns.
    - Coefficient ranges from -1 (perfect negative linear relationship) to +1
(perfect positive linear relationship).
  - Spearman's rank correlation:
    - Measures monotonic relationships by converting values to ranks first, then
applying Pearson correlation to the ranks.
    - Detects consistent directional patterns that may be curved (non-linear) but
still consistently increasing or decreasing.
  - Kendall's Tau:
    - Measures ordinal association by comparing how often pairs of observations
  agree in their ranking order.
    - More robust to outliers and better at detecting threshold effects where
  relationships change at certain values.

- **Key Differences in Plain Language:**

  - Pearson: "Are these variables connected in a straight-line pattern?"
  - Spearman: "Do these variables consistently move in the same direction, even if
  not in a straight line?"
  - Kendall: "Do these variables have similar ranking patterns, and is one a good
  predictor of the other's rank?"

- **Findings:**

  - All correlation coefficients across all three techniques were very weak (< 0.1).
  - This finding was consistent across both target variables
(`delay_probability`and `delivery_time_deviation`)

#### Phase 2

---

### 3. Results Summary and Interpretation

---

### 4. Possible Flaws

---

### 5. Possible Alternative Approaches

---

### 6. Replication and Files

---

### 7. Conclusion

---
