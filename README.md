# 🛒 Quick-Commerce Basket Value Optimizer: Maximizing Checkout Efficiency
**Target Platform Focus:** Zepto / Blinkit (Indian Quick-Commerce Ecosystem)  
**Project Domain:** Product Management Teardown, Behavioral Analytics & Feature Specification  

---

## 🚀 1. Executive Summary
In India's hyper-growth quick-commerce (Q-Commerce) market, profitability relies entirely on maximizing **Average Order Value (AOV)** to offset the fixed logistics costs of dark-store operations and rider payouts. 

A critical operational leak occurs directly on the cart review sheet. Users frequently build high-intent baskets that fall just short of the free delivery threshold (typically ₹299). When confronted with an unexpected ₹35–₹40 delivery charge, budget-conscious users experience immediate cognitive friction, leading to high rates of cart abandonment.

This project outlines the end-to-end product strategy for a **"Hit Free Delivery" Smart Widget** embedded directly into the cart bottom-sheet. By dynamically serving hyper-relevant, low-ticket, high-margin filler items that perfectly bridge the specific spending gap, the feature eliminates user browsing fatigue, lowers cart abandonment, and programmatically elevates platform AOV.

---

## 📉 2. Core Problem Statement & Market Friction
Internal user funnel logic across Q-commerce platforms exposes a recurring transaction barrier: **A major drop-off spike among users with active basket values sitting between ₹200 and ₹280.**

### The Broken User Journey:
1. **The Intent Stage:** A user selects essentials totaling ₹235.
2. **The Paywall Shock:** Upon opening the cart, the system flags a ₹35 delivery fee because the basket is ₹64 short of the free threshold.
3. **The Search Tax:** To avoid losing money to a delivery fee, the user wants to add a cheap "filler" item. However, the current UI forces them to exit the cart, return to the homepage, brainstorm an item costing exactly ~₹65, verify its availability in their local dark store, and re-add it.
4. **The Leak:** This multi-step backtracking causes decision fatigue. The user either abandons the purchase entirely or switches to a competitor's app to check if the delivery fee is lower.

---

## 📊 3. Data-Driven Insights & A/B Testing Results
To validate this problem, we analyzed a simulated dataset of **10,000 checkout sessions** focusing on the high-friction basket cohort (₹200 - ₹280). 

### 📈 Funnel Performance Matrix

| Metric Matrix | Control Group (Legacy Checkout UI) | Test Group (With Smart Filler Widget) | Performance Delta |
| :--- | :---: | :---: | :---: |
| **Cart Abandonment Rate** | **38.4%** | **14.2%** | **-24.2% (Drop-off Slashed)** |
| **Conversion Rate (Orders Paid)** | 61.6% | 85.8% | **+24.2% Conversion Lift** |
| **Average Order Value (AOV)** | ₹234.50 | ₹308.20 | **+₹73.70 AOV Growth** |
| **Total Gross Revenue** | ₹310,478 | ₹576,334 | **+85.6% Revenue Surge** |

> 💡 **Key Takeaway:** By removing the "Search Tax" and offering instant options, we successfully pushed average basket sizes up by **₹73.70**, driving massive top-line growth for the localized dark store while saving the user money on delivery fees.
> *Detailed log schemas can be reviewed in the [`data_analysis/`](./data_analysis/) directory.*

---

## 🛠️ 4. Feature Specifications & Algorithmic Logic
The feature is designed as an automated, dynamic UI element embedded directly into the checkout sheet.

### The Tri-Factor Recommendation Engine
1. **The Delta Filter ($\Delta$):** Calculates the exact spending gap: $\Delta = 299 - \text{Current Value}$. It only surfaces items where the price ($P$) satisfies: $\Delta \le P \le \Delta + ₹40$.
2. **The Affinity Filter:** Cross-references active items against an adjacency matrix (e.g., if cart has *Spicy Ramen*, prioritize a *Cold Beverage*).
3. **The Velocity Fallback:** Defaults to universal high-margin impulse items (*Chips, Soft Drinks, Chocolate Bars*) to optimize dark-store inventory clearance.

---

## 📐 5. Detailed Product Documentation
The deep-dive documentation detailing edge cases, technical wireframe guidelines, success tracking models, and guardrail metrics is hosted separately:

👉 **[Read the Full Product Requirement Document (PRD)](./documentation/functional_prd.md)**
