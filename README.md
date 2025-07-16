

# 🔐 DeFi Wallet Credit Scoring (Aave V2)

This project develops a machine learning-based credit scoring system for DeFi wallets based on transaction-level data from the Aave V2 protocol. It processes raw JSON logs to assign each wallet a score between 0 and 1000 — where higher scores indicate more reliable and responsible DeFi behavior.

📊 Goal: Help DeFi platforms identify trustworthy wallets and detect risky or bot-like actors.

---

## 📁 Project Structure

CreditScoring-RF/
│
├── .gitignore
├── CreditScoring.ipynb               # Main notebook containing the model implementation
├── README.md                         # Project overview and instructions
├── analysis.md                       # Additional analysis or insights
├── requirements.txt                  # Dependencies for the project
│
├── score_distribution_rf.png         # Output visualization (e.g., score distribution plot)
│
├── user-wallet-transactions.json     # Input data: user wallet transaction details
├── wallet_scores_rf.json             # Output data: credit scores predicted by the model
---

## 📦 Features Extracted per Wallet

From the raw JSON logs, the following features were engineered:

- Total number of transactions
- Number of unique action types (deposit, borrow, repay, redeem, liquidation)
- Sum of deposit, borrow, repay, and redeem amounts
- Liquidation event count
- Repay/Borrow ratio
- Borrow/Deposit ratio
- Bot-likeness: high volume but low action diversity
- Active time span (days between first and last transaction)

---

## 🧠 Scoring Logic

🛠️ Two scoring approaches were used:

1. Rule-Based Score (pseudo_score)

A transparent heuristic that rewards:
- Strong repay behavior (repay ≥ borrow)
- Diverse actions (≥ 4 unique types)
- No liquidations
- Balanced borrowing

And penalizes:
- Liquidation events
- Borrowing more than depositing
- Bot-like patterns

2. ML-Based Score (rf_score)

- Trained a RandomForestRegressor using the engineered features and the pseudo_score as a weak label
- Final scores were clipped to 0–1000 and saved to wallet_scores_rf.json
- Feature importance analysis included

---

## 📈 Visualization

The final score distribution across all wallets is shown below:

![Score Distribution](score_distribution_rf.png)

- Most wallets score between 600–800, indicating balanced and responsible usage.
- Scores below 300 usually signal bots, high-risk activity, or exploit behavior.
- High scorers (900–1000) are highly responsible and show repay-heavy and diverse behavior.

---

