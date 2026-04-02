# 🍴 Tasty Bytes — Recipe Traffic Prediction Model

> **DataCamp Data Scientist Professional Practical Exam**  
> A machine learning solution that predicts which recipes will drive high homepage traffic, replacing manual curation with data-driven decision-making.

---

## 📌 Project Overview

**Tasty Bytes** is a recipe subscription platform founded in 2020. Their Product Manager manually selects recipes to feature on the homepage each day — a process that takes ~2 hours and produces inconsistent results. A popular recipe drives up to **40% more sitewide traffic**, directly impacting subscriptions and revenue.

**This project builds a predictive model** that automatically identifies high-traffic recipes with ≥80% accuracy, enabling automated homepage curation and a projected **+35–40% traffic uplift**.

---

## 🎯 Business Requirements

| Requirement | Target | Achieved |
|-------------|--------|----------|
| High-Traffic Recall | ≥80% | ✅ 80% |
| Precision | ≥75% | ✅ 82% |
| Improvement vs Random | >0% | ✅ +32.8% |
| Ready for deployment | Week 1 | ✅ Yes |

---

## 📊 Dataset

**File:** `recipe_site_traffic_2212.csv` — 895 recipes, 8 columns

| Column | Type | Description | Missing |
|--------|------|-------------|---------|
| `recipe` | int | Unique recipe ID (dropped before modelling) | 0 |
| `calories` | float | Calories per serving | 52 |
| `carbohydrate` | float | Carbohydrates in grams | 52 |
| `sugar` | float | Sugar in grams | 52 |
| `protein` | float | Protein in grams | 52 |
| `category` | str | Recipe type (11 categories) | 0 |
| `servings` | str/int | Number of servings | 0 |
| `high_traffic` | str | Target: "High" if popular; else missing | 373 |

**Raw:** 895 rows · **Clean:** 843 rows (52 removed — all nutrition fields missing)

---

## 🔍 Key Findings

### Finding 1: Category is the Strongest Predictor

| Category | High-Traffic Rate | Recommendation |
|----------|-------------------|----------------|
| 🥕 Vegetable | **98.8%** | Always feature |
| 🥔 Potato | **94.3%** | Always feature |
| 🥓 Pork | **91.7%** | Always feature |
| 🍽 One Dish Meal | 73.2% | Often feature |
| 🥩 Meat | 74.7% | Often feature |
| 🍰 Dessert | 63.9% | Selective |
| 🥪 Lunch/Snacks | 64.0% | Selective |
| 🍗 Chicken Breast | 46.9% | Use caution |
| 🍗 Chicken | 36.5% | Use caution |
| 🍳 Breakfast | 31.1% | Use caution |
| ☕ Beverages | **5.4%** | Avoid |

### Finding 2: Hearty Recipes Win

| Nutrient | High-Traffic | Low-Traffic | Difference |
|----------|-------------|-------------|------------|
| Calories | 463.6 kcal | 394.9 kcal | +17% more |
| Protein | 25.5g | 22.2g | +15% more |
| Carbohydrate | 38.0g | 30.7g | +24% more |
| Sugar | 8.1g | 10.4g | -22% less |

---

## ⚙️ Model Results

| Metric | Logistic Regression ✅ | Random Forest |
|--------|----------------------|--------------|
| Accuracy | **78.8%** | 73.7% |
| Recall (High) | **80.0%** | 76.0% |
| Precision (High) | **82.0%** | 78.9% |
| AUC-ROC | **0.835** | 0.790 |
| F1-Score | **0.816** | 0.774 |

**Decision threshold tuned to 0.46** to achieve exactly ≥80% recall.

---

## 📁 Project Files

| File | Description |
|------|-------------|
| `predictive_model.html` | Project showcase webpage |
| `notebook.ipynb` | Full Python analysis notebook |
| `recipe_site_traffic_2212.csv` | Raw dataset (895 recipes) |
| `top_popular_recipes.csv` | Top 30 predictions |
| `README_tastybytes.md` | This file |

---

## 🛠️ Tech Stack

`pandas` · `numpy` · `matplotlib` · `seaborn` · `scikit-learn`  
Models: `LogisticRegression` · `RandomForestClassifier`  
Techniques: `StandardScaler` · `train_test_split` · `precision_recall_curve` · threshold tuning

---

## ▶️ How to Run

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
# Open notebook.ipynb in Jupyter or DataLab and run all cells
```

---

## 📋 Monitoring Plan

| Metric | Current | Target | Alert If |
|--------|---------|--------|---------|
| Recall (High) | 80% | ≥80% | <75% → retrain |
| Precision | 82% | ≥75% | <70% → investigate |
| Homepage CTR | Baseline | +35% | Drop → review |

**Retrain:** Monthly · **Monitor:** Weekly · **A/B Test:** First 30 days on 10% traffic

---

## ⚠️ Key Decisions

| Decision | Rationale |
|----------|-----------|
| Fill missing `high_traffic` as "Low" | Conservative: unexplored = likely not popular |
| Remove 52 all-missing nutrition rows | Cannot reliably impute when all 4 nutrition fields absent |
| Choose Logistic Regression | Better on all metrics; simpler and more interpretable |
| Tune threshold to 0.46 | Achieves ≥80% recall while keeping precision at 82% |

---

**Status:** ✅ Ready for Deployment · **Date:** December 2024  
**Exam:** DataCamp Data Scientist Professional Practical
