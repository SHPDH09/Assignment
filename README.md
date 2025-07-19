
## 🧠 Approach

We use a **transparent, rule-based scoring method** rather than a black-box ML model. This ensures trust, explainability, and fairness.

Each wallet is scored based on the following behavioral features:

- 📥 **Deposits**
- 💸 **Borrows and Repays**
- ⚠️ **Liquidations** (heavily penalized)
- 🔄 **Redemptions**
- 📊 **Token Diversity**
- 📆 **Active Days on Protocol**

---

## 🧮 Feature Definitions

| Feature              | Description                                  |
|----------------------|----------------------------------------------|
| `num_deposits`       | Number of deposit transactions               |
| `total_deposited`    | Total value deposited by wallet              |
| `num_borrows`        | Number of borrow transactions                |
| `total_borrowed`     | Total value borrowed                         |
| `num_repays`         | Number of repayments                         |
| `total_repaid`       | Total value repaid                           |
| `num_liquidations`   | Number of times wallet was liquidated        |
| `num_redemptions`    | Number of times assets were withdrawn        |
| `unique_tokens`      | Number of different tokens interacted with   |
| `activity_days`      | Number of unique days wallet was active      |

---

## 🧮 Scoring Logic

The score starts at a base of **500** and is adjusted as follows:

### ✔️ Positive Signals

| Behavior                     | Score Impact     |
|-----------------------------|------------------|
| Deposits/Repaid Volume      | +2 pts per 1k    |
| Deposit/Repay Count         | +2 pts each      |
| Token Diversity             | +2 pts per token |
| Active Days                 | +1 pt per day    |

### ❌ Negative Signals

| Behavior                     | Score Penalty    |
|-----------------------------|------------------|
| Each Borrow                 | -1 pt            |
| Each Liquidation            | -50 pts          |
| Each Redemption             | -1 pt            |

The score is clipped to stay within `[0, 1000]`.

---

## 🚀 How to Run

### 1. Install Python Dependencies

```bash
pip install -r requirements.txt
