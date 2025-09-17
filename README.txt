Predicting Customers’ Organic Product Purchase Decisions
A course project on predicting consumers’ decisions to buy organic products using exploratory data analysis (EDA), clustering, and supervised learning. The project uses a real dataset (~9,000 rows) collected in An Giang and Kien Giang (Viet Nam) to support segmentation and marketing strategy design for an organic-rice business case.

1) Project Overview

Goal: predict the binary target OrganicsPurchaseIndicator (0 = No, 1 = Yes) and extract actionable customer segments.

Context: rising health concerns and the growth of organic agriculture motivate better targeting and positioning for organic products.

Team/Affiliation: Ho Chi Minh City Open University, 2024; supervisor: Hồ Hướng Thiên.

Authors: Nguyễn Phát.

2) Data

Size: ~9,000 records (households), two provinces (An Giang, Kiên Giang).
Features:

Gender (0 = female, 1 = male)

Age (years)

AffluenceGrade (1–35, higher = more affluent)

LoyaltyCardTenure (years using retail loyalty cards)

TotalSpend (total customer spend)

OrganicsPurchaseIndicator (target: 0/1)

Observed class balance: about 18% “Yes” (positive class).

3) EDA Highlights

Demographics: females make up ~65.7% of respondents.

Age patterns: older groups (50–70) appear highly interested in organic products in descriptive charts; correlation analysis, however, shows a negative correlation between Age and purchase (see next section), suggesting further stratified analysis is needed.

Affluence distribution: most customers cluster around mid-affluence (e.g., 7–9), reflecting stable, non-affluent rural households as the core base.

4) Correlations (w.r.t. OrganicsPurchaseIndicator)

Gender: −0.13 (female consumers tend to buy more than male)

Age: −0.35 (negative association; younger purchase more in the correlation view)

AffluenceGrade: +0.34 (richer consumers buy more)

LoyaltyCardTenure: −0.047 (very weak)

TotalSpend: −0.099 (weak, negative)

Note: Descriptive EDA vs. correlation give mixed signals on age; we recommend segment-wise checks and model-based partial effects before drawing causal conclusions.

5) Unsupervised Segmentation (K-Means)

Elbow method suggests k = 6 clusters.

Clusters visualized on (Age, AffluenceGrade); representative centers (Age, Affluence) include examples like (30.0, 9.9), (39.1, 9.9), (57.1, 8.5), (65.8, 8.2), (74.6, 8.1), etc., indicating diverse age-income micro-segments.

6) Modeling

Algorithms: Random Forest (RF), Extreme Gradient Boosting (XGB), Logistic Regression (LR).

Accuracy (report):

RF: 83%

XGB: 85%

LR: 85%

Confusion Matrix (example model):

TP = 149, TN = 1,350, FP = 61, FN = 194 → Accuracy ≈ 85.5%

For the positive (“Yes”) class, recall is a concern in XGB/LR; RF chosen as the reference due to better recall on “Yes”.

Decision Tree (for interpretability)

k-fold cross-validated accuracy: 86.56%.

Top split drivers: AffluenceGrade → Age → LoyaltyCardTenure.

7) Actionable Segments (from Decision Paths)

Likely buyers (class = Yes), examples:

AffluenceGrade ≤ 9.5 and Age ≤ 37.5 (younger, less affluent but responsive)

TotalSpend > 15,644 and LoyaltyCardTenure > 7.5 (loyal spenders)

AffluenceGrade > 16.5 and LoyaltyCardTenure > 7.5 (affluent & loyal)

Less-likely buyers (class = No), examples:

TotalSpend ≤ 7,350 (very low spend)

AffluenceGrade ≤ 5.5 or Age > 44.5 in certain branches

AffluenceGrade > 12.5 with Age ≤ 39.5 (younger affluent segments needing different positioning)

8) How to Reproduce (suggested)

Environment

Python 3.10+, pandas, numpy, scikit-learn, matplotlib/plotly, scipy.

Steps

Load and clean data; check duplicates, missing, and types.

EDA: distributions, outliers, correlation, class balance.

Train/validate models (RF/XGB/LR); use stratified splits; report precision/recall/F1/AUC for the positive class.

Tune thresholds to improve recall on the minority “Yes” class.

Train a shallow Decision Tree for explainability (export rules).

Optional: K-Means (k=6) to label segments and compare conversion by cluster.

Deliverables

Notebook(s): eda.ipynb, modeling.ipynb, segmentation.ipynb

Plots: /figures

Report: /report (this README links high-level results)

9) Business Takeaways

Messaging and channels should be tailored to female decision-makers and affluent/loyal segments.

For segments with lower affluence but higher propensity (young households), position value & safety (health, “no chemicals”) at affordable pack sizes.

Track post-campaign lift by segment; iterate with A/B tests.

10) Limitations & Next Steps

Class imbalance (~18% “Yes”) affects recall; apply class weighting, SMOTE, or threshold tuning.

Resolve age-interest inconsistency via cohort analysis and interaction terms.

Add features (household composition, education, proximity to organic stores, price sensitivity).

Validate on a hold-out period or new province for robustness.

11) Acknowledgments

Ho Chi Minh City Open University — Course: Data Analysis; Instructor Hồ Hướng Thiên; Contributors: Vũ Ngọc Duy, Nguyễn Nguyên Ái Vân, Nguyễn Phát (student IDs in the report).
