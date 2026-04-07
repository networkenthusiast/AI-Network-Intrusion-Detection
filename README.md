# AI-Based Network Intrusion Detection System (Hybrid Model)

This project presents a **hybrid intrusion detection system (IDS)** that combines:

- Supervised learning (Random Forest)
- Unsupervised learning (K-Means Clustering)
- Meta-learning (XGBoost)

The goal is to improve detection performance by leveraging both **labeled patterns** and **hidden structures in network traffic**.

---

## 📁 Project Overview

The complete implementation is available in the notebook:

👉 :contentReference[oaicite:0]{index=0}

The project follows a **multi-stage machine learning pipeline**:

1. Data preprocessing & feature selection  
2. Supervised model (Random Forest)  
3. Unsupervised model (K-Means clustering)  
4. Feature aggregation  
5. Final hybrid model (XGBoost)

---

## 🧠 Model Architecture

### Model 1 — Random Forest (Supervised)

- Trained on labeled data
- Outputs:
  - `rf_pred` → predicted label
  - `rf_prob` → probability score

---

### Model 2 — K-Means (Unsupervised)

- Uses PCA-reduced features
- Clusters traffic into 2 groups
- Clusters mapped to labels using mean label values

Generated features:
- `cluster_pred`
- `cluster_dist_0`
- `cluster_dist_1`

---

### Model 3 — Hybrid Model (XGBoost)

- Combines:
  - Original features
  - RF outputs
  - Clustering outputs
- Uses feature selection + GridSearchCV

---

## ⚙️ Pipeline Flow

Raw Data
↓
Preprocessing
↓
Random Forest → rf_pred, rf_prob
↓
K-Means → cluster features
↓
Feature Aggregation
↓
XGBoost (Final Model)


---

## 📊 Results Summary

### K-Means (Unsupervised)

- Accuracy: ~83%
- AUC: ~0.65
- High recall for benign traffic
- Lower recall for attack class

👉 Provides **pattern-based signals** rather than precise classification

---

### Final Hybrid Model (XGBoost)

- Accuracy: ~100%
- AUC: ~0.9999
- Near-perfect precision & recall
- Strong generalization (validated via learning curves and CV)

---

## 📈 Key Insights

- Random Forest captures **known attack patterns**
- K-Means captures **hidden behavioral structure**
- XGBoost effectively **learns from both signals**

The hybrid approach significantly improves performance over individual models.

---

## 🔍 Feature Importance

- `rf_prob` is the most dominant feature
- Clustering distance features contribute additional signal
- Hybrid model learns strong interactions between features

---

## 🚨 Data Leakage Considerations

To ensure model reliability:

- Cross-validation used
- Learning curves analyzed
- Label shuffling test performed

⚠️ Note:
Feature generation (RF + clustering) must be done carefully to avoid leakage in production pipelines.

---

## ⚠️ Limitations

- Risk of leakage due to stacked features
- High dependency on engineered features
- Reduced interpretability
- Computationally intensive pipeline
- May not generalize to unseen attack types

---

## 🚀 Future Work

- Build fully leakage-safe pipeline (using sklearn Pipeline)
- Add deep learning models (LSTM / Autoencoders)
- Real-time streaming deployment
- Multi-class attack classification
- Explainability using SHAP / LIME
- Handle concept drift in evolving network data

---

## 🛠️ Tech Stack

- Python
- Pandas, NumPy
- Scikit-learn
- Random forest algorithm
- Clustering
- XGBoost
- Matplotlib

---

## 🧪 How to Run

1. Clone the repository
git clone https://github.com/networkenthusiast/AI-Network-Intrusion-Detection.git

2. Install dependencies
pip install -r requirements.txt

3. pip install -r requirements.txt


---

## 👨‍💻 Author

Kalyan Brata Majumder <br>
Karthik Mekala<br>
MS-Applied AI

---

## 📌 Conclusion

This project demonstrates how combining **supervised and unsupervised learning** can significantly enhance intrusion detection systems. While the hybrid model achieves excellent performance, careful handling of feature engineering and pipeline design is essential for real-world deployment.