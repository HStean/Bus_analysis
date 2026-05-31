# Predicting School Bus Usage in Abu Dhabi Private Schools

**Institution:** Sorbonne University Abu Dhabi  
**Tools:** R, tidyverse, caret, randomForest, ggplot2

---

## Overview

This project analyzes survey responses from **4,014 families** across Abu Dhabi, Al Ain, and Al Dhafra to predict whether a child uses the school bus 4+ days per week — and to identify the key factors that drive that decision.

The analysis was presented as a final project to a joint committee of officials from **ADEK (Department of Education and Knowledge)** and **ITC (Integrated Transport Centre)**.

---

## Key Findings

- **Distance is the strongest predictor.** Bus usage rises from 16% for families within 5 minutes of school to 88% for families more than 30 minutes away — a 45× increase in odds (logistic regression OR = 44.8, controlling for all other variables).

- **Curriculum group matters independently of logistics.** Indian CBSE families have ~4× higher odds of frequent bus use than American curriculum families, even after controlling for distance, car ownership, and income (OR = 3.95).

- **What families say they want:** Among 1,625 non-frequent bus users, 47% cited lower cost, 35% shorter routes, and 32% one-way trip options as the changes that would encourage them to switch — suggesting flexibility and pricing, not coverage, is the primary barrier.

---

## Models

Two predictive models were built and evaluated on a held-out test set (80/20 stratified split):

| Model | Accuracy | Sensitivity | Specificity | Kappa |
|---|---|---|---|---|
| Logistic Regression | 72.7% | 77.2% | 66.2% | 0.434 |
| Random Forest (ntree=500, mtry=4) | 84.8% | 90.2% | 76.9% | 0.680 |

The Random Forest substantially outperforms the logistic baseline by capturing non-linear thresholds and interaction effects between predictors.

---

## Methodology

- **Missing data:** Median imputation for numeric variables; mode imputation for categorical variables. All 4,014 rows retained.
- **Feature engineering:** Categorical variables (including `father_job` and `mother_job`) were factored before modelling to ensure correct treatment in the Random Forest.
- **Variable selection:** 16 predictors selected from 96 variables based on theoretical relevance to school transport behavior: distance, car ownership, curriculum, neighborhood, parental licenses, income, housing type, bus satisfaction ratings (cost, stop, reliability), and parental job categories.
- **Evaluation:** Both models evaluated on the same 803-row held-out test set for a fair comparison.

---

## Recommendations

Based on model findings and survey analysis:

1. **Pilot flexible, partial-week bus subscriptions** (one-way trips, custom-day plans, proportional pricing) in British, American, and MoE UAE schools — directly responding to the top survey signals.
2. **Engage non-Indian curriculum communities** by studying what makes the bus work so well for Indian CBSE families and replicating it in other school communities.
3. **Shorten the longest routes** — 35% of non-bus families said shorter routes would encourage them to switch.

---

## Files

| File | Description |
|---|---|
| `bus_analysis.Rmd` | Full R Markdown source — data prep, EDA, models, interpretation |
| `bus_analysis.html` | Knitted output with all plots and results |
| `presentation/` | Final slide deck presented to ADEK + ITC committee |

**Note:** The raw survey dataset is not included in this repository as it contains responses from private individuals and is the property of Sorbonne University Abu Dhabi.

---

## How to Run

1. Clone the repository
2. Obtain the dataset (contact the university)
3. Place `bus_analysis.csv` in the root directory
4. Open `bus_analysis.Rmd` in RStudio and knit to HTML

**Required R packages:**
```r
