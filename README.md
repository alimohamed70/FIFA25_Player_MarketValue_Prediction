# FIFA 25 — Player Market Value Prediction (Regression)

Predicting football player **market value (€)** from **FIFA 25 (SoFIFA 2025-06-03)** attributes using machine learning.

---

## ✨ Summary

- **Goal:** Estimate player market value from ratings, potential, age, wage, and club context.  
- **Final Model:** RandomForest (300 trees, `max_features='sqrt'`) on **log target** with **smearing** back-transform.  
- **Test Performance:** **R² = 0.932**, **RMSE ≈ €1.94M**, **MAE ≈ €0.30M**.  
- **Key Drivers:** `release_clause_eur`, `overall_rating`, `potential`, `wage_eur`, `age`, `club_rating`.  
- **Ablation (no release clause):** **R² = 0.875**, **RMSE ≈ €2.65M**, **MAE ≈ €0.45M** → release clause is a strong business signal.
---

## 🗂️ Data

- **Source:** Kaggle (SoFIFA snapshot)  
- **Dataset ID:** `aniss7/fifa-player-data-from-sofifa-2025-06-03`  
- **File used:** `player-data-full-2025-june.csv` (version `2025-06-03`)

> Note: Several granular skill attributes (e.g., `finishing`, `dribbling`, `sprint_speed`) are **100% missing** in this snapshot, so the model relies on robust available fields (ratings, wage, club rating, etc.).

---

## ⚙️ Setup

```bash
git clone <your-repo-url>
cd FIFA25_Player_MarketValue_Prediction
pip install -r requirements.txt
```

## 📊 Results

| Model                                | RMSE (log) | MAE (log) | R² (log) | RMSE € (smear) | MAE € (smear) | R² € (smear) |
|--------------------------------------|:----------:|:---------:|:--------:|:--------------:|:-------------:|:------------:|
| **RandomForest (Final, with release clause)** | **0.189**  | **0.074** | **0.976** | **€1,940,445** | **€304,095** | **0.932** |
| **RandomForest (Ablation, no release clause)** | 0.229      | 0.111     | 0.965     | €2,644,986      | €453,652      | 0.875       |

**Interpretation:** Including `release_clause_eur` improves accuracy (ΔR² **+0.057**, ΔRMSE **−€0.70M**).  
*Note:* Euro metrics use smearing correction when back-transforming from the log target.
