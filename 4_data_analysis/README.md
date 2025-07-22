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

- **Phase 1 Results:**

  - All correlation coefficients across all three techniques were very weak (< 0.1).

  - **Strongest Correlations by Technique for the Unmodified Data:**

    <!-- markdownlint-disable MD013 -->

| Method     | Target                   | Top Feature              | Correlation Factor |
|------------|--------------------------|--------------------------|--------------------|
| Pearson    | delay_probability        | port_congestion_level    | +0.0090            |
|            | delivery_time_deviation  | port_congestion_level    | +0.0106            |
|            | eta_variation_hours      | supplier_reliability_score | +0.0079          |
| Spearman   | delay_probability        | port_congestion_level    | +0.0067            |
|            | delivery_time_deviation  | port_congestion_level    | +0.0118            |
|            | eta_variation_hours      | lead_time_days           | -0.0087            |
| Kendall’s Tau | delay_probability    | route_risk_level         | -0.0046            |
|            | delivery_time_deviation  | port_congestion_level    | +0.0079            |
|            | eta_variation_hours      | lead_time_days           | -0.0058            |

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

- **Phase 2 Results:**

  - Correlation coefficients remained weak (< 0.1) even after data corrections,
indicating that measurement inconsistencies were not the primary cause of weak relationships.

  - **Strongest Correlations by Technique for the Modified Data:**

| Method     | Target                   | Top Feature                | Correlation Factor |
|------------|--------------------------|----------------------------|--------------------|
| Pearson    | delay_probability        | port_congestion_level      | +0.0089            |
|            | delivery_time_deviation  | port_congestion_level      | +0.0106            |
|            | eta_variation_hours      | supplier_reliability_score | +0.0078            |
| Spearman   | delay_probability        | route_risk_level           | -0.0065            |
|            | delivery_time_deviation  | port_congestion_level      | +0.0118            |
|            | eta_variation_hours      | lead_time_days | -0.0085           |
| Kendall’s Tau | delay_probability    | route_risk_level           | -0.0044            |
|            | delivery_time_deviation  | port_congestion_level / handling_equipment_availability     | +0.0079/ -0.0079            |
|            | eta_variation_hours      | lead_time_delays | -0.0067           |

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

- **Results:**
  - Interaction correlations remained weak (< 0.1), showing no improvement over individual factors.
  - **Multivariate Interaction Effects:**

Phase 1

| Target                  | Top Interaction Feature | Correlation Factor |
|-------------------------|-------------------------|--------------------|
| delay_probability       | port_x_customs          | +0.0096            |
| delivery_time_deviation | traffic_x_weather       | -0.00098           |
| eta_variation_hours     | route_x_driver          | -0.0038            |

Phase 2

| Target                  | Top Interaction Feature | Correlation Factor |
|-------------------------|-------------------------|--------------------|
| delay_probability       | route_x_driver     | -0.0038            |
| delivery_time_deviation | port_x_customs             | +0.0095             |
| eta_variation_hours     | route_x_driver                       | -0.0045                 |

---

### 3. Results Summary

Each method was applied to assess the relationships between 16 features and 3 target variables. Across all methods, the findings revealed consistently weak correlations. However, Spearman and Kendall methods demonstrated added robustness by capturing non-linear and ordinal associations.

Despite the overall weak correlations of individual features, combinations of features exhibited even lower correlation strength based on Pearson analysis.

In **Phase 1**, the feature **post_congestion_level** (indicating the level of port congestion) showed the highest correlation with delay—though the value remained very low.

In **Phase 2, port_congestion_level** again emerged as the most correlated feature, alongside the appearance of lead time and route risk. Although the correlation values were weak, port congestion was the most influential feature affecting delay across both phases.

In **the multivariate case**, the interaction between **port congestion and customs clearance time** yielded the highest correlation with delay probability, suggesting their combined effect plays a more significant role in predicting delays than individual features alone.

---

### Possible Flaws in the Analysis Strategy

1. **Multivariate Analysis is Limited to Linear Relationships**
   Pearson correlation only captures linear relationships. If the variables
   interact in nonlinear ways, important patterns may be overlooked.

2. **Lack of Normalization in Multivariate Analysis**
   No normalization or scaling was applied. Differences in variable units (e.g.,
   scores from 1–5 vs. 1–100) can distort results when multiplied.

3. **Overstated Effects of Individual Variables**
   A strong correlation in the multivariate results may be driven by one
   variable alone, rather than by the intended interaction effect.

4. **Manual Interaction Feature Selection**
   Interaction features were created manually. Potentially significant
   interactions may be missing.

5. **No Causal or Directional Analysis**
   The analysis did not explore causality or directionality, limiting deeper insights.

---

### 5. Possible Alternative Approaches

- **Use Nonlinear or Rank-Based Correlation**
  Incorporate Spearman or Kendall in multivariate analysis; also standardize
  features before interaction.

- **Apply Partial Correlation or Interaction-Aware Regression**
   Partial correlation and regression models with interaction terms can help
   isolate the effect of interactions after accounting for individual variables.

- **Automate Interaction Discovery**
  Use polynomial feature generation or tree-based models such as Random Forests
  that can naturally learn and evaluate interactions between features.

- **Explore Causal Relationships**
  If causality or direction matters, consider time-series-based methods like
  Granger causality or Structural Equation Modeling (SEM) for more advanced
  causal analysis.

---

### 6. Replication and Files

We followed a step-by-step process to clean and analyze the data. The relationship between the raw data, processed files, and notebooks is as follows:

#### 1. Raw Data Cleaning

- **Python File:** [clean_dataset.py](../2_data_preparation/clean_dataset.py)
- **Input:** [logistics_and_supply_chain.raw.csv](../1_datasets/raw_data/logistics_and_supply_chain.raw.csv)
- **Output:** [cleaned_dataset.csv](../1_datasets/cleaned_and_processed_data/cleaned_dataset.csv)

> This notebook was used to clean the original raw dataset by handling missing values, correcting inconsistent formats, and preparing it for analysis.

#### 2. Phase 1 Analysis

- **Notebook:** [Correlation_Analysis_Phase_1.ipynb](../4_data_analysis/notebooks/Correlation_Analysis_Phase_1.ipynb)
- **Input:** [cleaned_dataset.csv](../1_datasets/cleaned_and_processed_data/cleaned_dataset.csv)

> In this notebook, we used the cleaned dataset to perform Phase 1 of the correlation analysis using Pearson, Spearman, and Kendall methods.

#### 3. Phase 2 Analysis

- **Notebook:** [Correlation_Analysis_Phase_2.ipynb](../4_data_analysis/notebooks/Correlation_Analysis_Phase_2.ipynb)
- **Input:** [cleaned_secondApproach_dataset.csv](../1_datasets/cleaned_and_processed_data/cleaned_secondApproach_dataset.csv)

> For Phase 2, we further processed the cleaned data by correcting binary encoding and unit inconsistencies. The resulting processed dataset was then used in this notebook to re-run the correlation analysis.

---
