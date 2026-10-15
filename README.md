# Project Title: Coupon Acceptance Analysis

## Project Description
This repository contains a comprehensive Exploratory Data Analysis (EDA) investigating the factors that influence whether a driver will accept a coupon delivered to their smartphone. The analysis explores a dataset derived from the [UCI Machine Learning Repository](https://uci.edu), which was collected via surveys on Amazon Mechanical Turk. 

The survey tracks diverse driving attributes (e.g., destination, current time, weather, passenger types), driver demographics (e.g., age, occupation, gender, income), and specific behavioral patterns (frequency of visits to bars, coffee houses, and restaurants). Coupon types span across five distinct categories: less expensive restaurants (under \$20), coffee houses, carry out & take away, bars, and more expensive restaurants (\$20 - \$50).


## About the repository

**Repository location**: https://github.com/zalkap/BHPCMLAI_M5_Assignment

To run this repository locally, execute the following configuration steps:
```bash
# Clone the repository
git clone https://github.com/zalkap/BHPCMLAI_M5_Assignment.git
cd BHPCMLAI_M5_Assignment

# Install required dependencies
pip install pandas numpy matplotlib seaborn jupyter

# Initialize the Jupyter server
jupyter notebook
```


## Dataset & Data Cleansing Summary
The dataset (`coupons.csv`) consists of **12,684 records** across **26 feature columns**.
* **Baseline Acceptance Rate:** Out of all total observation scenarios, **56.84%** of drivers chose to accept the coupon (`Y = 1`).
* **Missing/Problematic Data Adjustments:**
  * **The `car` attribute** contained 12,576 null observations (accounting for ~99% of total entries). These missing values were programmatically imputed with the label `"data not provided"` to preserve structure without impacting subsequent analytical phases.
  * **Frequency-based features** (`Bar`, `CoffeeHouse`, `CarryAway`, `RestaurantLessThan20`, `Restaurant20To50`) exhibited missing entries accounting for roughly **6.26%** of total data rows. To ensure objective modeling and baseline purity, all row-level records containing these null values were entirely discarded.


## Summary of Findings

### 🍺 Investigating Bar Coupons
Bar coupons recorded an overall baseline acceptance rate of **41.00%** across the general sample population. Deep conditional subset filtering revealed the following critical insights:

* **Frequency is the Primary Predictor:** Prior behavioral habits act as the single strongest operational feature. Drivers who visit bars **more than 3 times a month** show an acceptance rate of **76.88%**, whereas occasional or non-visitors (3 or fewer times a month) settle at **37.06%**. Frequent bar patrons are over **2.07 times more likely** to accept.
* **The "Over-25" Factor:** Drivers older than 25 who visit a bar at least 1–3 times a month exhibit an increased acceptance probability of **69.52%**, contrasted against a low **33.50%** across all other blended demographics.
* **Environmental Constraints:** Active bar-goers who have **no child passengers** onboard and do **not** work in rural settings (e.g., *Farming, Fishing, or Forestry*) experience a spike up to **71.32%** acceptance. This proves that removing situational friction significantly unlocks conversion potential.
* **Irrelevant Signals:** General dining or saving habits are an exceptionally weak cross-signal predictor. Active patrons of cheap restaurants (≤ \$20) earning under \$50K only accepted bar coupons at a rate of **45.00%**, moving very slightly from the general baseline.

### ☕ Independent Investigation: Coffee House Coupons
Coffee house coupons recorded a dead-even overall baseline acceptance rate of **49.93%** (virtually a strict 50/50 split). Feature engineering uncovered highly localized behavioral spikes:

* **Age & Gender Variances:** While age segments generally follow uniform paths, extreme demographic outliers appear at the edges. **Male drivers under 21** and **at age 46** show a dramatically higher probability of accepting a coffee coupon compared to female drivers in identical brackets.
* **Temporal Patterns:** Time of day remains a primary determinant. Drivers are significantly more inclined to accept coffee offers during the **morning peak (10 AM)** compared to late-afternoon or late-evening intervals.
* **Climate & Direction Dynamics:** Environmental conditions display a distinct trend, showing increased coupon acceptance when the weather is **sunny but cold/chilly** outside. Conversely, geographical layout showed neutral significance; whether the venue was located in the **same direction** or the **opposite direction** of travel yielded no noticeable statistical change.


## Targeted Customer Hypotheses

Based on the statistical indicators aggregated above, optimizing distribution and maximizing marketing return-on-investment (ROI) requires shifting from wide broadcasting to specific consumer profile targeting:

* **Bar Coupon Strategy:** Target active adult bar-goers who drink at least once a month, driving alone or exclusively with adult peers (ensuring no children are present). Income limits or generic cost-conscious restaurant traits should be excluded from filters.
* **Coffee House Coupon Strategy:** Target the morning commute window (ideally around 10 AM), heavily favoring young or middle-aged male outliers, especially under chilly yet clear, sunny conditions.


