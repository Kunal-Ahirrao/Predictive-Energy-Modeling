---
title: "Energy Usage & Savings"
author: "IST 687 M002, Group No-5"
output:
  html_document: default
  pdf_document: default
---

# Energy Usage & Savings

## Technical Report Paper

**Energy Usage & Savings**

## Team Members

- Kunal Ahirrao  
- Sukhad Dnyanesh Joshi

## Table of Contents

1. [Project Overview](#project-overview)
2. [Describing the Data](#describing-the-data)
3. [Exploratory Analysis](#exploratory-analysis)
4. [Visualizing the Data](#visualizing-the-data)
5. [Modeling the Data](#modeling-the-data)
6. [Shiny App](#shiny-app)
7. [Modeling the Impact](#modeling-the-impact)
8. [Potential Approach to Reduce Peak Energy Demand](#potential-approach-to-reduce-peak-energy-demand)
9. [Conclusion](#conclusion)
10. [Work Log](#work-log)

## Project Overview

This project investigates energy consumption patterns with a focus on predicting and understanding energy usage and potential savings. By analyzing static house data, weather conditions, and hourly energy consumption, we aim to develop models that not only forecast energy usage but also offer insights into reducing peak energy demand. An interactive Shiny app is provided to help visualize the impact of various predictors on energy consumption, which can assist decision makers in planning and efficiency improvements.

## Describing the Data

The dataset for this project comprises three main data sources:

**Static House Data:**  
- Includes details such as number of floors, square footage, building characteristics, and geographic location.  
- *Note: Data was originally stored in a .parquet format and imported using `read_parquet()`.*

**Weather Data:**  
- Contains daily measurements for temperature, wind speed, humidity, etc., recorded over the month of July.

**Energy Consumption Data:**  
- Records hourly energy usage for over 5,170 houses across approximately 171 columns, later merged with the other datasets to analyze daily energy trends.

A custom function, `process_energy_data()`, was developed to streamline the ingestion of multiple building IDs into R for further analysis.

## Exploratory Analysis

Initial analysis steps included:

**Data Overview:**  
- Using `head()` to inspect the first few rows of the dataset.  
- Employing `tail()` to view the last few rows for an end-of-data snapshot.  
- Utilizing `str()` to understand the structure, variable types, and names.  
- Running `summary()` to extract statistical insights (mean, min, max, etc.) across variables.

These steps helped in identifying the key variables and understanding the overall data quality before proceeding to modeling.

## Visualizing the Data

Visualization techniques played a crucial role in understanding data distribution and identifying patterns:

**Histograms:**  
- Displayed the distribution of `daily_total_usage`.  
  - Noted that while usage values range from -25 to 100, the majority lie between 20 and 30 units.  
  - Extreme values near -25 to 0 and 90 to 100 are negligible.

**Square Footage Analysis:**  
- A histogram of `in.sqft` showed a right-skewed distribution with most values between 0 and 3500, with a noticeable peak in the 1500–2000 range.

**Bedrooms Distribution:**  
- Visualization of the number of bedrooms per house revealed that most houses contain 3 bedrooms, followed by 4 bedrooms, and fewer houses with only 1 bedroom.

These visualizations helped to pinpoint variables that may significantly impact energy consumption.

## Modeling the Data

After data visualization, a linear regression model was built to forecast energy usage:

**Data Preparation:**  
- The dataset was split into training (80%) and testing (20%) subsets to ensure reproducibility (using a fixed seed).

**Initial Model:**  
- A multiple linear regression model was created using all available variables.  
- Model diagnostics (e.g., p-values) were used to refine the model by selecting significant predictors.

**Refined Model Insights:**  
- Key drivers include house square footage, climate zone, type of electronic appliances used, and household poverty levels.  
- The model provided a quantifiable peak energy demand prediction, which is critical for capacity planning.

Example code snippet:

set.seed(123)
# Splitting data into training and testing
train_index <- sample(1:nrow(data), 0.8 * nrow(data))
train_data <- data[train_index, ]
test_data <- data[-train_index, ]

# Building the linear regression model
model_lm <- lm(energy_usage ~ ., data = train_data)
summary(model_lm)

# Predicting energy demand
predicted_energy_demand <- predict(model_lm, newdata = test_data)
peak_energy_demand <- max(predicted_energy_demand)


# Shiny App

An interactive Shiny web application was developed to allow users to explore the impact of various predictors on energy usage. Key features include:

### Input Controls:
- `selectInput` for categorical variables (e.g., type of dryer, climate zone).
- `sliderInput` for quantitative variables (e.g., temperature, humidity).

### Output:
- A dynamic prediction display showing how adjustments in predictor variables affect the forecasted energy usage.
- Useful for decision-makers (e.g., CEOs) to visually assess which factors contribute most to energy consumption.

**Access the Shiny App here:**  
[Energy Usage & Savings Shiny App](https://sjoshi12.shinyapps.io/Final_app_IDS/)

# Modeling the Impact

Beyond forecasting, the project also explores the potential effects of modifying building attributes on energy demand:

### Simulation of Changes:
- Reductions in square footage and adjustments in appliance data (e.g., cooking range) were modeled.

### Outcome Assessment:
- The resulting shifts in predicted peak energy demand highlight how targeted modifications can lead to significant energy savings.

This analysis provides actionable insights for stakeholders interested in reducing energy consumption through building efficiency improvements.

# Potential Approach to Reduce Peak Energy Demand

Based on our analysis, several strategies have been identified to mitigate peak energy usage:

### Energy-Efficient Appliances:
- Promote the use of energy-saving washers, dryers, and cooking appliances.

### Operational Shifts:
- Encourage off-peak usage to reduce high-demand periods.

### Improved Building Design:
- Enhance insulation and HVAC systems, especially in mixed-humid climates.
- Advocate for smaller, more energy-efficient home designs.

### Renewable Integration:
- Consider installing solar panels to offset peak demand by generating renewable energy during high-sunlight periods.

### Incentives:
- Implement subsidies or incentives for households to invest in energy-efficient technologies.

# Conclusion

This project provides a comprehensive analysis of energy consumption and potential savings by integrating detailed building, weather, and energy usage data. The linear regression model, supplemented by visual analytics and an interactive Shiny app, offers valuable insights into the drivers of energy consumption. Ultimately, the findings support the development of strategies that promote sustainable energy practices and reduce peak demand through both technological and behavioral interventions.

# Work Log

- **Kunal Ahirrao** – Coding, Shiny app, Visualizations and document  
- **Sukhad Dnyanesh Joshi** – Coding, Modeling and document
