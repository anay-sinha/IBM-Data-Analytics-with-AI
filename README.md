# Lichess Chess Analytics

An end-to-end exploratory and predictive data analytics project analyzing **19,113 unique online chess games** from Lichess to evaluate first-move advantage, calibrate empirical Elo dynamics, assess opening performance, and benchmark pre-game outcome prediction.

## 📌 Project Summary

* **Project Title:** Lichess Chess Analytics

* **Dataset:** 20,058 raw games (Aug 2013 – Sep 2017) $\rightarrow$ 19,113 unique games post-audit.

* **Core Stack:** Python, Pandas, NumPy, SciPy, Scikit-Learn, Matplotlib, Seaborn.

* **Primary Objective:** Determine what factors genuinely predict game outcomes prior to move 1, and benchmark them against classical chess theory.

## 📚 Dataset Source 

**Kaggle Link:<a id="[implementation-details](https://www.kaggle.com/datasets/datasnaek/chess)"></a>**
    
## 🎯 Key Findings

| Metric / Question | Key Result | Takeaway | 
 | ----- | ----- | ----- | 
| **White Advantage** | **52.4%** decisive win rate (95% CI: 51.6%–53.1%) | Consistent across all rating tiers and time controls ($p < 10^{-10}$). | 
| **Empirical Elo Scale (**$k$**)** | $k = 0.64$ (95% CI: 0.61–0.67) | Ratings are flatter than standard Elo ($k=1.0$); upsets happen more often. | 
| **White Advantage Value** | $\approx 22$ **rating points** | Validated via custom loss minimization and logistic regression odds. | 
| **Game Resolution** | 56% resign, 31% mate, 8% timeout, 4% draw | Faster controls triple timeout rates (12.3% in $<10$m vs 4.0% in \$25+$m). | 
| **Opening Residuals** | English (+4.5%) & Bishop's (+6.4%) overperform | Most major lines track rating expectations within $\pm 2\%$. $1.e3$ underperforms by $-8.9\%$. | 
| **Outcome Prediction** | **65.1% Accuracy / 0.718 AUC** | Rating gap carries almost all signal. Openings/speed add negligible predictive lift. | 

## 🛠️ Data Audit & Cleaning Decisions

1. **Deduplication:** Identified and removed 945 identical duplicate records (4.7%), leaving 19,113 clean games.

2. **Clock Telemetry:** 43% of rows had identical start and end timestamps. Game duration was standardized to **full moves** ($\lceil\text{turns} / 2\rceil$).

3. **Time Controls:** Analyzed time controls revealed no Bullet and minimal Blitz. Games were categorized into duration bins: `<10 min`, `10–15 min`, `15–25 min`, and `25+ min`.

4. **Leakage Prevention:** Models strictly evaluate pre-game features (`rating_diff`, `avg_rating`, `time_class`, `game_type`, `opening_family`, `first_move`). Post-game metrics (`turns`, `victory_status`) were strictly excluded.

## 🔬 Predictive Modeling Benchmarks (5-Fold CV)

| Model & Feature Set | Accuracy | ROC-AUC | Log-Loss | 
 | ----- | ----- | ----- | ----- | 
| **Baseline (Class Prior)** | 52.37% | 0.5000 | 0.6920 | 
| **Logistic Regression (`rating_diff` only)** | **65.14%** | **0.7177** | **0.6152** | 
| **Logistic Regression (+ Speed, Tier, Type)** | 65.20% | 0.7172 | 0.6155 | 
| **Logistic Regression (+ Openings & 1st Move)** | 64.97% | 0.7169 | 0.6150 | 
| **HistGradientBoosting (All Features)** | 64.79% | 0.7156 | 0.6136 | 

## 📂 Repository Structure

```
├── games.csv                                 # Dataset (20k games)
├── AnaySinha_LichessChessAnalytics.ipynb     # Complete analysis & visualizations
├── README.md                                 # Project documentation
├── requirements.txt                          # Dependencies
├── Anay Sinha_ProjectReport.docx             # Comprehensive 10-page final project report
└── chess_game-analysis.html                  # Exported HTML version of Jupyter Notebook

```

## ⚡ Quickstart

1. **Clone the repository:**

   ```
   git clone https://github.com/anay-sinha/IBM-Data-Analytics-with-AI-Lichess-Chess-Analytics.git
   cd IBM-Data-Analytics-with-AI-Lichess-Chess-Analytics
   
   ```

2. **Install requirements:**

   ```
   pip install -r requirements.txt
   
   ```

3. **Run the analysis:**

   ```
   jupyter notebook AnaySinha_LichessChessAnalytics.ipynb
   
   ```
