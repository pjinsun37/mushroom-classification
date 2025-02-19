# mushroom-classification

# ‼️ Problem
Mushroom foraging has grown in popularity, but with it comes an increased risk of mushroom poisoning. From January to October 2023, America’s Poison Centers reported an 11% rise in poisoning cases compared to 2022. Given the severe health consequences of misidentification, this project utilizes historical data to develop a model that can accurately classify mushrooms as edible or poisonous.

# 💡 Solution

We leveraged machine learning models that balance interpretability and predictive accuracy. Three models were implemented to evaluate this tradeoff:

**1. Decision Tree Classifier (Glassbox Model)**
- A simple, interpretable model that splits data based on feature thresholds.
- Prioritizes clarity in decision-making but may sacrifice predictive accuracy.

**2. Random Forest Classifier (Blackbox Model)**
- An ensemble of decision trees that enhances performance through bagging.
- Improves generalization but reduces interpretability.

**3. XGBoost Classifier (Blackbox Model)**
- A gradient boosting model optimized for high performance.
- The best model in terms of precision and recall but requires interpretability techniques like SHAP.


**⚠️ Risk-Aware Model Design: Adjusted Loss Function**
- Since misclassifying a poisonous mushroom as edible is far riskier than the reverse, we adjusted the classification loss function to penalize false negatives more heavily
- Class Weights: This adjustment ensures that models prioritize identifying poisonous mushrooms correctly, significantly reducing high-risk errors.
  - Edible (Class 0): Weight = 1
  - Poisonous (Class 1): Weight = 5

<p>&nbsp;</p>

# 🔎 Key Findings
- XGBoost achieved 100% recall on poisonous mushrooms, making it the best model despite its blackbox nature.
- Using SHAP for interpretability: Odor-related features were the most significant predictors of toxicity.

<p>&nbsp;</p>

# 📊 Dataset

- The dataset consists of 8,124 mushrooms, each characterized by 22 categorical attributes (i.e. Cap shape, Odor, Gill size, Habitat)
- The target variable is class, where (e = Edible, p = Poisonous)
- The dataset is nearly balanced (4,208 edible vs. 3,916 poisonous), eliminating the need for resampling techniques.

(Source: Kaggle)

<p>&nbsp;</p>

# 🔧 Data Preprocessing

- Encoding Categorical Features: One-Hot Encoding was applied to convert categorical variables into a numeric format.
- Label Encoding Target Variable: e (edible) → 0, p (poisonous) → 1
- Data Splitting: 0%-20%-20% with stratification to maintain class distribution

<p>&nbsp;</p>

# 🏆 Model Evaluation & Results

**Evaluation Metrics**
- To prioritize risk mitigation, we focused on:
  - Recall: % of actual poisonous mushrooms correctly classified (false negatives should be minimized!)
  - Precision: % of predicted poisonous mushrooms that were actually poisonous
  - Confusion Matrix: Detailed breakdown of true/false positives and negatives

**Results**
- Decision Tree: 99% recall (4 misclassified), 100% precision
- Random Forest: 100% recall, 100% precision
- XGBoost: 100% recall, 100% precision

✅ XGBoost is the optimal choice, offering perfect classification with SHAP-based interpretability.

<p>&nbsp;</p>

# 🔎 Interpretability with SHAP
Since XGBoost is a blackbox model, we used SHAP (Shapley Additive Explanations) to understand feature contributions at both global and local levels.


**Global Interpretability**

SHAP summary plots reveal the most influential features in classification:
- Odor → strongest indicator of toxicity
- Gill size → Large gills correlate with edibility
- Bruising presence → Lack of bruises correlates with poisonous mushrooms

<img width="874" alt="Screenshot 2025-02-20 at 12 57 21 AM" src="https://github.com/user-attachments/assets/4e19dc84-710d-4018-948b-3ca115b423f7" />

<p>&nbsp;</p>

**Local Interpretability (Individual Predictions)**

- Largest contributing features towards this prediction are the lack of an odor and the absence of bruises.

<img width="958" alt="Screenshot 2025-02-20 at 12 56 59 AM" src="https://github.com/user-attachments/assets/494b286a-0841-4c4d-8a58-c2c0e67c18b6" />


