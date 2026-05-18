# 🚲 Yulu Bike Sharing Demand Analysis

## Business Problem

Yulu — India's leading micro-mobility provider — experienced a significant decline in revenues and needed to understand what drives demand for their shared electric cycles. This project identifies the key factors affecting bike rental demand using Exploratory Data Analysis and Statistical Hypothesis Testing.

**Two core business questions answered:**
1. Which variables significantly affect the demand for shared electric cycles?
2. How well do these variables explain rental demand patterns?

---

## Dataset Overview

| Feature | Description |
|---|---|
| datetime | Hourly timestamp of rental |
| season | 1: Spring, 2: Summer, 3: Fall, 4: Winter |
| holiday | Whether the day is a public holiday |
| workingday | Whether the day is a working day |
| weather | 1: Clear → 4: Heavy Rain/Snow |
| temp | Temperature in Celsius |
| humidity | Humidity level |
| windspeed | Wind speed |
| count | Total bike rentals (target variable) |

**Dataset size:** 10,886 records, 12 columns. No null values or duplicates found.

---

## Tools & Libraries

- **Python** — Pandas, NumPy
- **Visualisation** — Matplotlib, Seaborn
- **Statistics** — SciPy (T-Test, ANOVA, Kruskal-Wallis, Chi-Square, Shapiro-Wilk, Levene)

---

## Key EDA Findings

- **Clear weather dominates rentals** — the vast majority of rides occur in weather category 1 (clear/partly cloudy)
- **Winter is the most popular season** for Yulu rentals, followed by Fall, Summer, and Spring
- **Strong multicollinearity detected** — `atemp` and `temp` had near-perfect correlation (removed `atemp`); `registered` and `casual` were subcomponents of `count` (removed to avoid data leakage)
- **Windspeed outliers** treated using IQR method; `count` outliers retained as they represent genuine demand spikes

---

## Hypothesis Testing — Results Summary

### Test 1: Weekday vs Weekend Demand
**Method:** 2-Sample T-Test (after Shapiro-Wilk normality check + QQ plot)

| | Result |
|---|---|
| H₀ | Weekday demand ≥ Weekend demand |
| Hₐ | Weekday demand < Weekend demand |
| P-Value | > 0.05 |
| **Decision** | **Fail to Reject H₀** |

**Finding:** No statistically significant difference in demand between weekdays and weekends. Yulu bikes are used consistently throughout the week.

---

### Test 2: Demand Across Weather Conditions
**Method:** Kruskal-Wallis Test (used because Shapiro-Wilk and Levene tests failed — data not normally distributed and variances not equal)

| | Result |
|---|---|
| H₀ | Average demand is equal across all weather conditions |
| Hₐ | Average demand differs across weather conditions |
| P-Value | < 0.05 |
| **Decision** | **Reject H₀** |

**Finding:** Weather significantly impacts bike rental demand. Clear weather drives meaningfully higher demand than misty or rainy conditions.

---

### Test 3: Demand Across Seasons
**Method:** Kruskal-Wallis Test

| | Result |
|---|---|
| H₀ | Demand is equal across all seasons |
| Hₐ | Demand differs across seasons |
| P-Value | < 0.05 |
| **Decision** | **Reject H₀** |

**Finding:** Season significantly affects rental demand. Winter and Fall show higher demand patterns than Spring.

---

### Test 4: Weather Dependency on Season
**Method:** Chi-Square Test of Independence

| | Result |
|---|---|
| H₀ | Weather conditions are independent of season |
| Hₐ | Weather conditions depend on season |
| P-Value | < 0.05 |
| **Decision** | **Reject H₀** |

**Finding:** Weather and season are not independent — weather patterns vary significantly across seasons, confirming both variables carry overlapping demand signals.

---

## Business Recommendations

1. **Seasonal pricing strategy** — Increase fleet availability and reduce per-ride pricing in Winter and Fall to capitalise on peak demand periods. Consider premium pricing in Spring when demand is lowest.

2. **Weather-based dynamic pricing** — Implement real-time pricing adjustments tied to weather forecasts. Offer discounted rides 24 hours before predicted clear weather windows to drive pre-booking behaviour.

3. **Weekday activation campaigns** — Since weekday and weekend demand are statistically similar, Yulu should not over-invest in weekend-only promotions. Focus instead on consistent daily engagement — loyalty rewards, commuter subscriptions, and corporate tie-ups.

4. **Station placement optimisation** — Given that weather and season jointly influence demand, Yulu should prioritise covered station infrastructure in high-demand zones to reduce weather sensitivity and extend the riding season.

5. **Predictive demand model** — The significant relationships found between weather, season, and demand provide a strong foundation for a machine learning demand forecasting model. Implementing this would allow Yulu to optimise fleet distribution before demand spikes rather than reacting to them.

---

## Project Structure

```
Yulu-Data-Analysis/
│
├── data/
│   └── bike_sharing.csv
├── Yulu_case_study.ipynb
└── README.md
```

---

## Author

**Aryan Gupta**  
Data Analytics | Python | Statistics | Hypothesis Testing  
[GitHub](https://github.com/aryan-gupta1404) | [LinkedIn](https://www.linkedin.com/in/aryan-gupta1404)
