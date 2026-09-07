# Recipe Site Traffic Prediction

A data science practical exam project: predicting whether a recipe will drive **high traffic** when featured on the Tasty Bytes homepage, to help the Product Manager choose recipes more strategically instead of relying on personal preference alone.

## Business Problem

Tasty Bytes features one recipe on the homepage each day. Featuring a popular recipe boosts site-wide traffic by up to 40% — but there was no systematic way to predict in advance whether a given recipe would perform well.

**Goal:** Predict which recipes will drive high traffic, correctly at least 80% of the time.

## Data

`data/recipe_site_traffic_2212.csv` — 947 recipes with nutrition info, category, servings, and traffic outcome.

Key cleaning steps:
- Merged a duplicate category label (`Chicken Breast` → `Chicken`)
- Cleaned inconsistent text in `servings` (`"4 as a snack"` → `4`)
- Recoded missing `high_traffic` values as `Low` (per the data's documented logic)
- Dropped 52 recipes missing all nutrition data (~5.5% of the dataset)

Final cleaned dataset: **895 recipes**.

## Approach

- **Problem type:** Binary classification (High vs Low traffic)
- **Baseline model:** Logistic Regression
- **Comparison models:** Decision Tree, XGBoost

## Results

| Model | Precision (High) | Recall (High) | Accuracy |
|---|---|---|---|
| **Logistic Regression** | **82.5%** | 75% | 75% |
| Decision Tree | 76% | 66% | 68% |
| XGBoost | 79% | 69% | 70% |

**Logistic Regression** was selected as the final model — the simplest model outperformed both tree-based alternatives, and cleared the Product Manager's 80% precision target.

## Business Impact

- Baseline (picking recipes without any predictive method): **59.8%** chance of High traffic
- With the model: **82.5%** precision
- ~23 percentage point improvement over uninformed selection

## Key Finding

Recipe **category** is a far stronger predictor of traffic than nutritional content:
- Vegetable, Potato, Pork: 90%+ High traffic
- Beverages, Breakfast: under 31% High traffic
- Correlation between nutrition variables (calories, sugar, etc.) and traffic: negligible (all under 0.1)

## Recommendations

1. Deploy the model — it already exceeds the 80% target
2. Immediate no-cost win: prioritize Vegetable, Potato, and Pork recipes
3. Use the model to rank candidates by predicted probability, keeping the Product Manager's final creative say

## Repository Structure

```
recipe-site-traffic/
├── notebook.ipynb          # Full analysis: data validation, EDA, modeling, evaluation
├── data/
│   └── recipe_site_traffic_2212.csv
├── images/                 # Charts generated during analysis and presentation
└── requirements.txt
```

## Tools Used

Python, pandas, numpy, scikit-learn, xgboost, matplotlib, seaborn
