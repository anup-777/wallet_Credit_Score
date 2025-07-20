# wallet_Credit_Score
# Aave V2 Wallet Credit Scoring

This project generates a **credit score (0–1000)** for wallets interacting with the [Aave V2](https://aave.com/) DeFi protocol, based solely on historical transaction behavior. It helps distinguish responsible users from risky, inactive, or potentially bot-driven wallets.

---

## Methodology

We use **unsupervised machine learning (KMeans clustering)** on wallet behavior to segment users into behavioral groups. Each cluster is mapped to a score range between 0 and 1000, 
We use unsupervised machine learning (KMeans clustering) to identify patterns in wallet behavior. KMeans groups wallets into distinct clusters based on features like transaction frequency, liquidation events, and repayment activity — without requiring labeled data.

Each cluster represents a different behavioral profile, which we then map to a credit score range (0–1000). Wallets in clusters showing responsible usage patterns (e.g., regular deposits, repayments) receive higher scores, while erratic or high-risk behavior (e.g., frequent liquidation, low activity) results in lower scores.
where:
- **Higher scores** indicate consistent, responsible usage (e.g., regular deposits, repayments, no liquidation)
- **Lower scores** suggest risky behavior (e.g., frequent liquidations, low activity, irregular usage)

---

## Architecture Overview

user-wallet-transactions.json (raw JSON)
│
▼
Feature Engineering (per wallet)

Action counts
Txn frequency
Days active
Avg time gaps
│
▼
Behavioral Clustering (KMeans)
│
▼
Score Assignment (0–1000 by cluster)
│
├──> wallet_credit_scores.csv
└──> score_distribution.png

----

##  Data Processing Flow

1. **Load Raw Data** from JSON file.
2. **Aggregate Wallet Behavior**:
   - Count `deposit`, `borrow`, `repay`, `redeem`, `liquidation`
   - Calculate days active, transaction frequency, time gaps
3. **Standardize Features** using `StandardScaler`.
4. **Cluster Wallets** using KMeans (`n_clusters=5`).
5. **Assign Scores** to each cluster (e.g., risky cluster → 200, responsible → 1000).
6. **Output Results**:
   - `wallet_credit_scores.csv`
   - `score_distribution.png` (graph)
   - `analysis.md` (wallet behavior insights)
