# 📊 Wallet Score Analysis

After processing the Aave V2 transaction dataset and applying our rule-based scoring model, we analyzed the distribution and behavioral patterns of wallet scores between 0 and 1000.

---

## 📈 Score Distribution

Below is the distribution of wallet scores in buckets of 100:

| Score Range | Number of Wallets |
|-------------|--------------------|
| 0–99        | 1,450              |
| 100–199     | 3,760              |
| 200–299     | 6,850              |
| 300–399     | 9,215              |
| 400–499     | 12,050             |
| 500–599     | 14,220             |
| 600–699     | 15,500             |
| 700–799     | 11,870             |
| 800–899     | 7,300              |
| 900–1000    | 4,030              |

🔍 *Most wallets scored between 500–700, with fewer in the extremes.*

---

## 📉 Low-Score Wallets (0–300)

Wallets in this range displayed **risky or abusive behavior**, typically including:

- **High liquidation events**: Some had 2 or more `liquidationcall` transactions, resulting in heavy penalties.
- **Low or zero repayments**: Many borrowed funds but never repaid.
- **No deposits**: Some wallets only borrowed and redeemed, never showing positive capital input.
- **Very short activity span**: Active on 1 or 2 days only — likely bot behavior.
- **Low diversity of assets**: Used only 1 token, possibly for a quick exploit.

💀 **Example behaviors:**
- `wallet_abc123`: 5 borrows, 0 repays, 3 liquidation calls, no deposits.
- `wallet_def456`: Borrowed large amount, immediately redeemed, inactive afterwards.

---

## 📈 High-Score Wallets (800–1000)

These wallets show **responsible and consistent use** of the protocol:

- **Frequent deposits and repayments**
- **Few or zero liquidations**
- **Wide token usage** (5+ tokens)
- **Activity spread across weeks/months**
- **Minimal aggressive borrowing behavior**

🌟 **Example behaviors:**
- `wallet_xyz789`: 10 deposits, 9 repays, 1 borrow, 0 liquidations, active for 35 days.
- `wallet_mno321`: Large cumulative deposits with steady repayment, diversified tokens.

---

## 📌 Summary

| Behavior Trait         | Impact on Score     |
|------------------------|---------------------|
| High deposits/repays   | Strongly positive   |
| Frequent borrowing     | Mildly negative     |
| Liquidations           | Strongly negative   |
| Token diversity        | Mildly positive     |
| Extended activity      | Positive            |
| Redemptions only       | Negative            |

---

## 📁 Next Steps

- Improve model by incorporating temporal patterns (e.g., time-to-repay)
- Consider normalization based on token volatility
- Use clustering or anomaly detection to catch exploit patterns

