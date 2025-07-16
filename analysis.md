# 📊 Credit Score Analysis (Random Forest)

This document presents an analysis of the wallet scores predicted using a Random Forest model trained on transaction-level data from the Aave V2 protocol.

---

## 🧠 Score Distribution

Wallet scores were binned into the following ranges:

- 0–99  
- 100–199  
- 200–299  
- 300–399  
- 400–499  
- 500–599  
- 600–699  
- 700–799  
- 800–899  
- 900–1000

![Score Distribution](score_distribution_rf.png)

---

## 🔍 Observations by Score Range

- ✅ 900–1000:  
  - These wallets demonstrate responsible DeFi usage.
  - High repay-to-borrow ratios.
  - Broad transaction diversity across deposit, borrow, repay, and redeem.
  - No liquidations.

- 👍 700–899:
  - Healthy wallets with diverse and frequent activity.
  - Occasional liquidations or imbalance, but overall good behavior.

- ⚠️ 500–699:
  - Moderate credit behavior.
  - May lack repay history or show signs of centralization.
  - Could benefit from more action diversity.

- ❌ 0–499:
  - Often exhibit high borrow-to-deposit ratios.
  - Some were liquidated or performed only a few types of actions.
  - High risk or bot-like pattern.

---

## 📈 Insights

- Repay Ratio and Transaction Diversity were highly influential features.
- Wallets with limited actions (e.g., only deposit + withdraw) tended to receive lower scores.
- Liquidation events had a strong negative weight in both rule-based and ML models.

---

## ✅ Conclusion

The Random Forest model enhances credit scoring by learning complex interactions between features extracted from DeFi behavior. This approach provides a robust and scalable alternative to rule-based scoring, while preserving interpretability.

The final scores (wallet_scores_rf.json) can be used in DeFi credit evaluation pipelines, loan platforms, or on-chain reputation systems.
"""
