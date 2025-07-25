# I. Problem Statement & Background Research

In today’s rapidly evolving retail landscape, timely delivery is no longer a
luxury—it’s an expectation. The U.S. retail supply chain faces growing pressure
from consumers who demand faster delivery, especially in urban areas. Despite
advancements like real-time tracking and same-day shipping, many retailers
still struggle with delivery delays that harm customer satisfaction and
increase business costs.

Our team chose to focus on the U.S. retail supply chain because of its
widespread impact and complex, data-rich nature. We’re especially interested in
identifying the factors that cause delays and how predictive analytics and
machine learning can help mitigate them. We began our journey by exploring a
dataset that provides logistics and transportation data from Southern
California—an ideal testbed given the region’s high traffic volume and dense
delivery activity.

## II. Research Questions

### 🔍 Main Research Question

What are the key factors contributing to delivery delays in the retail supply
chain, and how can they be mitigated using data-driven methods?

### 📌 Supporting Questions

- How do traffic congestion, weather, and warehouse constraints influence
  delivery times?
- Can we predict delivery delays using machine learning models based on
  environmental and logistics data?
- How do seasonal events or unpredictable disruptions (like COVID-19 or winter
  storms) affect last-mile deliveries?
- What features are most strongly correlated with delay probability?

### III. Data Preparation, Exploration and Modelling Strategy

For our project, we selected the Southern California Supply Chain Dataset from
among several candidates. This dataset captures supply chain operations over
the period from January 2021 to January 2024.

During the data preparation phase, our primary objective was to understand the
dataset’s structure, quality, and overall characteristics before moving on to
more advanced analysis and modelling.

The dataset contains a total of 32,066 rows and 26 columns, encompassing a wide
range of features related to transportation logistics, warehouse management,
route planning, and real-time monitoring. It was sourced from Kaggle, and
according to its description, the data was aggregated from various systems,
including GPS tracking systems, IoT sensors, warehouse management systems, and
external data providers. The dataset covers multiple modes of
transportation—such as trucks, drones, and rail—and offers valuable insights
into operational efficiency, risk factors, and service reliability.

## Activities We Performed at the Data Preparation Phase

- **Data Loading**: The dataset is loaded into memory using standard Python
  tools, such as `pandas`, without modifying the source file. All exploration is
  done in-memory to preserve data integrity.

  ![Figure I](images/figure_1.png)

- **Descriptive Statistics**: Basic statistics are computed to understand
  central tendencies, variability, and data completeness. This includes
  examining the mean, median, standard deviation, minimum and maximum values,
  and missing data counts.

![Figure II](images/figure_2.png)

- **Data Cleaning**: We removed some irrelevant columns to focus on useful
  features. We also confirmed there are no missing values or duplicate rows.

## Activities We Performed at the Data Exploration Phase

During the Data Exploration phase, we conducted a correlation analysis of the
dataset features to identify potential factors contributing to delivery delays.
As we explored the data in more depth, we encountered several inconsistencies
between the dataset and its description on Kaggle. Additionally, some of the
data values appeared to be inaccurate or illogical, raising concerns about data
quality. The detailed analysis is presented below.

### 📊 Feature Comparison Table

| Feature            | Kaggle Description           | Our Description           |
|--------------------|------------------------------|---------------------------|
| Timestamp          | The date and time when the   | Date and time of the      |
|                    | data was recorded (hourly    | observation               |
|                    | resolution)                  |                           |
| Vehicle GPS        | The latitude coordinate      | Latitude coordinate of the|
| Latitude           | indicating the location of   | vehicle                   |
|                    | the vehicle                  |                           |
| Vehicle GPS        | The longitude coordinate     | Longitude coordinate of   |
| Longitude          | indicating the location of   | the vehicle               |
|                    | the vehicle.                 |                           |
| Fuel Consumption   | The rate of fuel consumption | Fuel consumed per hour or |
| Rate               | recorded for the vehicle in  | mile (unit likely in      |
|                    | liters per hour.             | liters or gallons)        |
| ETA Variation      | The difference between the   | difference between        |
| (hours)            | estimated and actual arrival | expected and actual       |
|                    | times.                       | arrival time              |
| Traffic Congestion | The level of traffic         | Scaled indicator of real- |
| Level              | congestion affecting the     | time traffic (e.g., 0–10) |
|                    | logistics route (scale       |                           |
|                    | 0-10).                       |                           |
| Warehouse          | The current inventory levels | Number of units/items in  |
| Inventory Level    | at the warehouse (units).    | warehouse                 |
| Loading/Unloading  | The time taken for loading   | Time taken to load/unload |
| Time               | or unloading operations in   | cargo                     |
|                    | hours.                       |                           |
| Handling Equipment | Availability status of       | Based on the description  |
| Availability       | equipment like forklifts (0  | in Kaggle, the dataset    |
|                    | = unavailable, 1 =           | should be 0 = unavailable,|
|                    | available).                  | 1 = available, however, it|
|                    |                              | is in scale from 0 to 1   |
| Order Fulfillment  | Status indicating whether    | Proportion of fulfilled   |
| Status             | the order was fulfilled on   | orders (0–1) / Based on   |
|                    | time (0 = not fulfilled, 1 = | the description in Kaggle,|
|                    | fulfilled).                  | the dataset should be 0 = |
|                    |                              | unavailable, 1 =          |

While the dataset offers a rich variety of features for analyzing supply chain
logistics, several data quality issues were identified that may affect modeling
accuracy and interpretation. First, certain features deviate from their
expected value ranges. For example, `weather_condition_severity` is expected to
range between 0 and 1 yet contains values exceeding 1. Similarly,
`route_risk_level` is described as a 0–1 scale but appears to range from 0
 to 9. The `order_fulfillment_status`, which should be binary (0 or 1), shows
fractions. The `cargo_condition_status` feature also exhibits decimal values
instead of the expected binary format. Moreover, `iot_temperature` includes
implausibly low temperatures for regions like California (e.g., –10°C),
suggesting either sensor errors or unit misinterpretation. The
`shipping_costs` field lacks a clearly defined currency, despite being
described in USD.

To understand the impact of these inconsistencies, we split the correlation
analysis into two phases:

1. Data Analysis based on the dataset as-is
2. Data Analysis after modifying the dataset according to the Kaggle
   description

## IV. Analysis / Findings

## Phase I

We used the dataset without modification and analyzed 32,065 supply chain
records to understand which operational factors are most strongly associated
with delivery delays. Using three different statistical methods (Pearson,
Spearman, and Kendall correlations), we tested 16 operational factors against 3
delay indicators to find the strongest relationships.

However, all correlations were remarkably weak. The strongest relationship we
found was only 0.0118 between port congestion and delivery time deviation. To
put this in perspective, correlation values range from -1 (perfect negative
relationship) to +1 (perfect positive relationship), so 0.0118 is extremely
close to zero.

> This chart shows that even our "strongest" correlations across all three
> statistical methods are extremely weak.

![Figure III](images/figure_3.png)

## Phase II

This study explored the key factors contributing to delivery delays in the U.S.
supply chain using a comprehensive dataset of logistics and operational
variables.

Contrary to common assumptions, our analysis showed that no single factor alone
can reliably predict delivery delays. Features like port congestion, supplier
reliability, and driver fatigue had only very weak individual correlations with
delay outcomes. However, when multiple risk factors occurred together—such as
bad weather combined with poor driver behavior or low inventory combined with
customs delays—the likelihood and severity of delivery delays increased
significantly.

These “compound risk” scenarios support the idea of cascading disruptions
described in supply chain literature, often referred to as the ripple effect
(Jusda, 2023; IMF, 2022).

While our findings are robust and consistent across different correlation
methods, they come with limitations. For example, our analysis was
cross-sectional and did not account for how delays evolve over time. We also
recognize that real-time data, like IoT sensor signals, might offer predictive
value when used dynamically, even if they don’t correlate strongly in static
analysis.

Our results suggest that improving supply chain reliability requires
system-level coordination, not isolated fixes. Visual tools like heatmaps and
interaction plots can help stakeholders identify and respond to these complex
patterns.

The analytical approach involved a multi-method correlation framework, using
Pearson, Spearman, and Kendall’s Tau to evaluate how operational,
environmental, and behavioral factors relate to delivery performance. The
consistent outcome across all three methods was that bivariate relationships
between individual features and delay outcomes were negligible—with most
correlation values close to zero.

This indicates that delivery delays are not the result of isolated variables,
but rather the interaction of multiple moderate-risk factors. We conducted
manual interaction analysis by evaluating how combinations of features behave
together under different scenarios. For instance, combinations like high port
congestion and low equipment availability, or fatigued drivers and adverse
weather, were associated with the most severe delivery time deviations.

These findings mirror established supply chain theories that emphasize
nonlinear dependencies and disruption propagation (MIT SCM, 2023; SDCExec,
2023).

A notable methodological choice was our decision not to use machine learning;
instead, we prioritized clarity through descriptive and
correlation-based methods.

However, as a potential alternative approach, machine learning—particularly
decision-making trees or ensemble models—could be used in future work to
automatically detect interactions, model nonlinear effects, and predict risk in
real time. These models, especially when paired with clarity techniques
like SHAP, could enhance predictive capability while maintaining transparency
(Küp et al., 2024).

Incorporating time-series analysis would also be valuable, as delay effects
often unfold over time—something not captured in our current static framework.

![Figure IV](images/figure_4.jpeg)

![Figure V](images/figure_5.jpeg)

### Conclusion

This analysis aimed to identify operational features most associated  
with delivery delays by applying correlation analysis across various  
techniques. While all individual and interaction-based correlations  
were consistently weak (typically < 0.01), several patterns emerged.

Notably, **port congestion level** consistently ranked as the top  
correlated feature across both original and corrected datasets. In  
Phase 2, additional features such as **lead time** and **route risk**  
began to appear more prominently. Despite the weak correlations,  
these features—particularly port congestion—emerged as the most  
influential within the limitations of the dataset.

Multivariate interaction analysis reinforced this observation, as  
the combination of **port congestion** and **customs clearance time**  
yielded the strongest (yet still weak) association with delay  
probability.

Overall, while no strong predictors of delay were identified, the  
repeated appearance of **port congestion level** suggests it plays a  
comparatively more central role in delay dynamics. Future work using  
more advanced, nonlinear, or causal modeling techniques may uncover  
deeper insights beyond the limitations of basic correlation analysis.
