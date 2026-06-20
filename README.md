# 🏥 Healthcare Utilization & Financial Risk Analytics
> **An End-to-End Analytics Solution Bridging Python Exploratory Data Analysis and Executive Power BI Portfolio Design.**

---

## 📋 Project Overview
This repository delivers a comprehensive analytics pipeline designed to unmask the critical cost drivers behind medical insurance claims. Portfolios in managed healthcare often face hidden financial volatility due to non-linear relationships between demographic profiles and medical billing. 

This project bridges technical backend data engineering with executive-ready business intelligence. The workflow transforms raw insurance assets via **Python (Pandas, Seaborn)** to isolate hidden risk profiles and maps those structural insights into a production-ready **Power BI Executive Dashboard** tailored for underwriting strategy and operations management.

---

## 🛠️ Tools Used
This project bridges technical backend data processing with executive business reporting using the following core tools:

* 🐍 **Python:** Main programming language used to build the data cleaning logic.
* 🐼 **Pandas:** Used for data manipulation, handling missing data types, grouping text categories, and building analysis grids.
* 📊 **Seaborn & Matplotlib:** Used during exploratory analysis to plot statistical charts, distributions, and outliers.
* 📈 **Power BI:** Used to build the final interactive dashboard, manage automated cross-filters, and style the user interface.
* 📐 **DAX (Data Analysis Expressions):** Used to write secure, custom business formulas to track population risk percentages on the fly.
* 🐙 **Git & GitHub:** Used for project version control, folder structuring, and portfolio hosting.
---

## 🔍 Core Analytical Breakthroughs & Data Stories

### 1. The Right-Skewed Bimodal Cost Distribution
A deep dive into the continuous distribution of the portfolio's claims reveals that medical charges do not follow a standard, symmetrical normal distribution. Instead, the data is heavily right-skewed with a significant **secondary bimodal peak between $35,000 and $50,000**. 
* **The Baseline Peak ($1k - $15k):** Represents standard, low-cost outpatient utilization and routine encounters.
* **The Secondary Hump ($35k - $50k):** Unmasks a specialized high-utilization sub-population driving the majority of portfolio spending volatility.

### 2. The Compounding Risk Vector (Obesity × Smoking)
Multi-variable relational plotting isolates the exact patient segments living inside that expensive secondary bimodal hump: **Obese Smokers**. While advanced age and high BMI independently cause linear increases in medical claims, their intersection with smoking status triggers an exponential compounding financial spike.

### 3. Regional Hotspot Isolation: The South East
Geographic patient density mapping shows uniform volume distribution across most territories, with one critical anomaly: **The South East region represents a compounding risk cluster**. It presents a 55% spike in absolute smoker density paired with the portfolio's highest concentration of clinically obese patients (249 individuals), flagging it as the primary engine for high-cost financial exposure.

---

## 📊 Power BI Dashboard Architecture
The companion Power BI report transforms static data insights into a highly responsive, executive-facing interface. 

### 📈 Core Portfolio Metrics (DAX Engine)
> **Total Financial Exposure** > `SUM(df[Charges])` — Total gross claims volume managed across the active portfolio.
>
> **Average Cost per Insured Individual** > `AVERAGE(df[Charges])` — Actuarial baseline cost per active member.
>
> **Overall High-Risk Population %** > Custom DAX measure tracking risk-asset concentration density to dynamically flag high-risk enrollment segments:
> ```dax
> Overall High-Risk Population % = 
> VAR TotalPatients = COUNTROWS('insurance')
> VAR HighRiskPatients = 
>     CALCULATE(
>         COUNTROWS('insurance'),
>         'insurance'[Smoker] = "yes" || 'insurance'[BMI_Range] = "Obese"
>     )
> RETURN
>     DIVIDE(HighRiskPatients, TotalPatients, 0)
> ```

### 🖥️ Strategic Reporting Canvas Layout
| Visual Target | Component Type | Business Purpose |
| :--- | :--- | :--- |
| **Medical Claims Distribution** | Binned Column Histogram | Maps continuous claims spread into \$5k increments to track shifting bimodal humps via live cross-filters. |
| **Regional Patient Density** | Matrix Heatmap Grid | Correlates geographic region against clinical BMI ranges, instantly highlighting regional risk concentration colors. |
| **Risk Factor Financial Variance** | Clustered Column Chart | Profiles the compounding dollar delta between smokers and non-smokers across BMI segments to guide underwriting strategies. |
| **Portfolio Slicers Panel** | Interactive Dropdowns | Allows operations managers to cross-filter the entire canvas dynamically by *Region*, *Smoking Status*, and *Age Category*. |

---
