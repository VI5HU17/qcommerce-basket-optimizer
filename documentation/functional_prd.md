# Product Requirement Document (PRD)
## Feature: Dynamic "Smart Filler" Basket Optimizer
**Status:** Proposed  
**Target Platform:** Zepto / Blinkit  
**Author:** Aspiring Analyst / Product Manager  

---

## 1. Feature Objective & Business Value
The objective of the **Smart Filler Widget** is to provide real-time, low-friction checkout interventions for users who are just below the free delivery threshold (₹299). 

### Business Impact:
*   **Primary Metric:** Increase Average Order Value (AOV) across target baskets by 8–12%.
*   **Secondary Metric:** Reduce checkout-stage cart abandonment rate by 15%.
*   **Margin Optimization:** Prioritize the recommendation of high-margin impulse items (Snacks, Beverages, Confectionery) to offset the cost of waiving the delivery fee.

---

## 2. Core Functional Logic & Backend Rules
The widget will operate using a three-tier algorithmic filter to determine which three items to surface to the user on the cart page.

### Rule 1: The Delta Price Match ($\Delta$)
Let $T$ be the free delivery threshold (₹299) and $V$ be the current user cart value. The system calculates the spending gap ($\Delta$):
$$\Delta = T - V$$

The widget will *only* surface items where the individual item price ($P$) satisfies the optimal pricing window:
$$\Delta \le P \le \Delta + ₹40$$

*Example: If a user's cart is ₹240, the gap ($\Delta$) is ₹59. The widget will display items priced between ₹59 and ₹99.*

### Rule 2: Category Affinity & Impulse Filtering
To ensure near-zero user hesitation, the recommendation engine will restrict its pool to three high-velocity, impulse-buy categories:
1.  **Beverages** (e.g., Cold soft drinks, juices, energy drinks)
2.  **Snacks & Savories** (e.g., Potato chips, nachos, instant noodles)
3.  **Sweet Cravings** (e.g., Chocolates, ice creams, single-serve cookies)

If the active cart already contains items from these categories, the engine will prioritize complementary affinity pairings (e.g., if the cart contains *Spicy Ramen*, recommend a *Cold Beverage* to balance it).

### Rule 3: Live Dark-Store Inventory Check
The widget must perform a real-time stock check against the user's localized dark store. If an item's stock count is less than 5 units, it is excluded from the widget to prevent post-checkout substitution friction.

---

## 3. UI/UX & Wireframe Requirements

The design must emphasize speed and minimal disruption to the checkout flow.

### A. Core UI Components
*   **The Progress Micro-Animation:** A bright visual progress bar positioned directly below the cart list. It dynamically fills up as items are added, accompanied by a quick text string: *"You are just ₹X away from saving ₹35 on delivery!"*
*   **Horizontal Carousel:** A clean, horizontal swipeable cards layout containing exactly 3 recommended items matching the logic rules.
*   **Single-Tap "Quick Add" Button:** Each product card must feature an instantaneous `+ ADD` action button. 

### B. Crucial Interaction Rule (Low-Friction Execution)
Tapping the `+ ADD` button **must not** trigger a full-page reload, loading spinners, or navigate the user away from the checkout screen. The item must visually "slide" into the cart list instantly, the progress bar must hit 100% (turning green), and the delivery charge line item must immediately drop to ₹0.

---

## 4. Success and Guardrail Metrics

To prove the feature's success, product analysts will track the following key performance indicators (KPIs):

| Metric Type | Metric Name | Definition / Target |
| :--- | :--- | :--- |
| **North Star** | Widget Conversion Rate | % of users exposed to the widget who tap `+ ADD` and complete checkout. |
| **Business Impact** | Delta AOV | The increase in average order value for users who interact with the widget vs. a control group. |
| **Guardrail** | Time-to-Checkout | The total time spent on the cart page. *Target: Must not increase by more than 5 seconds (ensuring the widget doesn't cause decision paralysis).* |
| **Technical** | Micro-Service Latency | The time it takes for the backend to surface the 3 recommendations. *Target: Under 150ms.* |
