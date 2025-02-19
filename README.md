# mushroom-classification
This project explores machine learning models for classifying mushrooms as edible or poisonous, emphasizing the trade-off between model interpretability and predictive performance. Given the fatal consequences of misclassifications, we adjust the classification loss function to prioritize identifying poisonous mushrooms correctly. Additionally, we apply SHAP (Shapley Additive Explanations) to improve interpretability for black-box models like XGBoost.

**Dataset**
- Source: Kaggle
- Size: 8,124 instances, each with 22 categorical features (e.g., cap shape, odor, gill size).
- Target Variable:
-   Edible (e) → 4,208 samples
-   Poisonous (p) → 3,916 samples
- Preprocessing Steps:
-   One-Hot Encoding for categorical variables
-   Label Encoding (0 for edible, 1 for poisonous)
-   Train-Test-Validation Split: 60%-20%-20% with stratification
