# Healthcare Utilization & Financial Risk Analytics

## 📋 Project Overview
This project delivers an end-to-end data analytics solution focused on unmasking the key cost drivers behind medical insurance claims. By bridging technical backend data engineering with executive-ready business intelligence, the project reveals how demographic risk vectors, geographic utilization hotspots, and compounding health behaviors translate into financial exposure.

The workflow translates raw, non-linear insurance portfolio data via **Python (Pandas, Seaborn)** into structural insights, culminating in an interactive **Power BI Executive Dashboard** engineered for underwriting and operations management.

---

## 🔍 Core Analytical Breakthroughs & Insights

### 1. The Right-Skewed Bimodal Cost Distribution
Analysis of the `Charges` distribution reveals that medical costs do not follow a standard normal distribution. Instead, they form a heavily right-skewed pattern with a significant **secondary bimodal peak between $35,000 and $50,000**. 
* **The Main Peak:** Represents standard, low-cost outpatient utilization.
* **The Secondary Hump:** Unmasks a specialized high-utilization sub-population. 

### 2. The Compounding Risk Vector (Obesity + Smoking)
Cross-tabulation and risk-stratification metrics isolate the exact profile of the patients living inside that expensive secondary hump: **Obese Smokers**. While obesity or smoking independently cause linear increases in claims, their intersection triggers an exponential financial spike.

### 3. Regional Hotspot Isolation: The South East
Geographic patient density mapping shows uniform population distribution across most territories, with one critical anomaly: **The South East region has a compounding risk profile**, presenting a 55% spike in absolute smoker density paired with the portfolio's highest concentration of clinically obese patients (249 individuals). This isolates the South East as the primary engine for high-cost financial exposure.

---

## 📊 Power BI Dashboard Architecture
The companion Power BI report transforms these data insights into a responsive, executive-facing interface. 

### Key Performance Indicators (KPIs) Built:
* **Total Financial Exposure:** Total gross claims volume across the active portfolio.
* **Average Cost per Insured Individual:** The actuarial baseline cost.
* **Overall High-Risk Population %:** A custom DAX measure tracking the concentration density of high-risk assets:
  ```dax
  Overall High-Risk Population % = 
  VAR TotalPatients = COUNTROWS('insurance')
  VAR HighRiskPatients = 
      CALCULATE(
          COUNTROWS('insurance'),
          'insurance'[Smoker] = "yes" || 'insurance'[BMI_Range] = "Obese"
      )
  RETURN
      DIVIDE(HighRiskPatients, TotalPatients, 0)
