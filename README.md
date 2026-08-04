# Calgary Property Value Prediction

Predicting **property value per square metre** in Calgary using regression, KNN, and tree-based models.

## Overview

Uses parcel-level data from the **City of Calgary Open Data Portal** to understand what drives property values — both **prediction** (how well can we estimate value?) and **interpretation** (what actually matters?).

**Core finding:** property value is primarily driven by location and nearby market context, not just property characteristics.

## Data

- Source: City of Calgary property assessments
- ~10M raw rows → cleaned + sampled dataset (~118k rows)
- Target: `VALUE_PER_SM`, modeled as `log(VALUE_PER_SM)`

## Features

- **Location** — latitude, longitude, distance to centre
- **Local market** — nearby median value
- **Property** — type, class, age
- **Density / community context**

## Models

- **Ridge / Lasso** — baseline, interpretable
- **KNN** — local comparables approach
- **Random Forest / Gradient Boosting** — nonlinear models (multi-year)

## Results

| Model | Validation R² |
|---|---|
| Ridge / Lasso | ~0.72 |
| **KNN (k=5)** | **0.83** |
| Gradient Boosting | ~0.73 |
| Random Forest | ~0.69 |

👉 KNN performs best — supports the idea that **valuation is a local spatial problem**.

## Key Insights

- Location dominates (lat/long are top features), and nearby properties drive most of the predictive power
- Property-specific features add relatively little once location is known
- Global models underperform local methods

## Limitations

- Potential spatial leakage (nearby properties in train/test)
- Limited external features (no macro / census data)
- Tree models constrained by runtime

## Next Steps

- Spatial holdout validation
- Add economic / demographic features
- Explore time-series / lag features

## Tech Stack

Python, pandas, scikit-learn, Jupyter

## Authors

Chris Petrauskas · Javier Becaria
