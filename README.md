# Lab 1: Phishing URL Detection — EDA, Logistic Regression & SHAP Explainability

**Institution:** ENSIASD Taroudant — Ibn Zohr University  
**Master:** Intelligent Systems and Cyber Defense (MSSIC)  
**Module:** M115 — AI & Intelligent Systems  
**Academic Year:** 2026–2027

---

## 📌 Objective

Build and interpret a machine learning pipeline to detect phishing URLs using lexical, network, and HTML features extracted from 235,795 real-world URLs.

---

## 📂 Files

| File | Description |
|------|-------------|
| `M115_Lab1_Template.ipynb` | Main notebook with all solutions |
| `PhiUSIIL_Phishing_URL_Dataset.csv` | Dataset (235,795 URLs, 56 features) |

---

## 📊 Dataset

**PhiUSIIL Phishing URL Dataset**  
- 235,795 URLs: 134,850 Legitimate + 100,945 Phishing  
- 56 features: lexical (URL structure), network (HTTPS, redirects), and HTML (password field, copyright, social links)  
- Source: Prasad & Chandra, *Computers & Security*, 2024  
- [View on Kaggle](https://www.kaggle.com/datasets/kaggleprollc/phishing-url-websites-dataset-phiusiil)

---

## 🧪 Lab Structure

### Part 1 — Security-Oriented EDA
- **Exercise 1:** Remap label so `1 = Phishing`, `0 = Benign` (SOC convention)
- **Exercise 2:** Visualize class balance, binary security indicators (`IsHTTPS`, `HasPasswordField`, `HasCopyrightInfo`, `HasSocialNet`), and numerical distributions (`URLLength`, `CharContinuationRate`, `NoOfSelfRef`)
- **Exercise 3:** Drop identifier columns, build feature matrix `X` and target `y`, compute Pearson correlations

### Part 2 — Zero-Data Leakage Preprocessing
- **Exercise 4:** Stratified 75/25 train-test split + fit `StandardScaler` on training data only

### Part 3 — Parameterized Logistic Regression
- **Exercise 5:** Train and compare 5 configurations (Unregularized, Strong L2, Standard L2, Sparse L1, Class-Weighted)
- **Exercise 6:** L1 regularization path — number of active features vs. C
- **Exercise 7:** Interpret log-odds weights `w_j` and odds ratios `exp(w_j)`

### Part 4 — Explainable AI (SHAP) & Threshold Tuning
- **Exercise 8:** Global SHAP explanations (Bar + Beeswarm plots) using `shap.LinearExplainer`
- **Exercise 9:** Local SOC triage — Waterfall plots for True Positive, True Negative, and False Positive cases
- **Exercise 10:** Operational threshold tuning at τ ∈ {0.20, 0.50, 0.85}

---

## 📈 Key Results

| Model | F1-Score | Recall | False Alarms (FP) |
|-------|----------|--------|-------------------|
| M1: Unregularized | ~0.97 | ~0.97 | low |
| M2: Strong L2 (C=0.001) | ~0.93 | ~0.92 | low |
| M3: Standard L2 (C=1.0) | ~0.97 | ~0.97 | low |
| M4: Sparse L1 (C=0.01) | ~0.96 | ~0.96 | very low |
| M5: Class-Weighted | ~0.97 | ~0.98 | higher |

---

## 🔑 Key Findings

- **HTTPS is not a reliable phishing indicator** — ~60-70% of phishing sites use valid TLS certificates
- **L1 regularization** eliminates 30+ features with minimal F1 loss — ideal for real-time firewall deployment
- **Top phishing indicators:** `HasPasswordField`, `NoOfURLRedirect`, `NoOfImage`
- **Top benign indicators:** `HasCopyrightInfo`, `HasSocialNet`, `IsHTTPS`
- **Recommended SOC policy:** Auto-block at τ = 0.85, human review for τ ∈ [0.20, 0.85)

---

## 🔗 Links

- 📓 Kaggle Notebook: [Kaggle : https://www.kaggle.com/code/mohamedamsount/lab01-ai-s7-ensiasdt](#)

---

## 🛠️ Tools & Libraries

`Python 3` · `Pandas` · `NumPy` · `Scikit-learn` · `Matplotlib` · `Seaborn` · `SHAP`
