# 🚢 Titanic Survival Visualisation

**Dataset:** Titanic passenger records | **Tool:** R

## Overview
Data wrangling and visualisation project exploring survival patterns in the Titanic dataset. The key challenge was engineering a `Gender` feature from messy passenger name titles — then using it to uncover survival differences by gender, passenger class, and marital status.

## 🎯 Key Findings

| Analysis | Finding |
|---|---|
| Survival by gender | **Females survived at significantly higher rates** than males |
| Survival by class | **1st class passengers** had the highest survival rate |
| Female marital status | Married and unmarried females showed different survival patterns |
| Male marital status | **Insufficient data** — "Mr" title gives no marital status information |

## 📊 Visualisations
- Stacked bar chart: Survival by gender
- Bar chart: Survival by passenger class
- Bar chart: Female survival by marital status (Miss vs Mrs)

## 🛠️ Tech Stack
- **Language:** R
- **Libraries:** `ggplot2`, `forcats`, `dplyr`
- **Data:** Titanic.csv passenger dataset

## 🔍 Methodology

### Feature Engineering — Gender Column
Extracted titles from passenger names using regex:
```r
titanic$Title <- sapply(titanic$Name, FUN = function(x) {
  regmatches(x, regexec(",  (.*?) ", x))[[1]][2]
})

Female_titles <- c("Miss", "Mrs", "Madame", "Lady", "Ms")
titanic$Gender <- ifelse(titanic$Title %in% Female_titles, "Female", "Male")
```
This produced **32 unique title categories** before mapping to binary gender.

### Visualisations Built
1. **Survival by Gender** — Stacked bar chart using `fct_reorder()` and `geom_bar(position="stack")`
2. **Survival by Class** — Bar chart ordered by survival count descending
3. **Female survival by marital status** — Miss vs Mrs/Madame/Lady

## 💡 What I Learned
Feature engineering from unstructured text fields is a common real-world challenge. This project also highlighted the importance of acknowledging data limitations — for males, the "Mr" title provides no marital status, so that analysis was correctly flagged as inconclusive rather than forced.

---
*Part of my data analytics portfolio — [view all projects](https://github.com/Jahnavi0605)*
