# From Raw Data to Revenue Insights: A Customer Behavior Analytics Dashboard (Python → SQL → Power BI)

An end-to-end retail analytics project — cleaning and preparing raw customer transaction data in Python, answering ten core business questions in SQL, and delivering the findings through an interactive Power BI executive dashboard.

## Executive Summary

This project analyzes **3,900 customer transactions** to uncover what drives revenue, retention, and loyalty in a retail business. The full pipeline spans Python (data cleaning and feature engineering), SQL (business-question answering), and Power BI (interactive executive dashboard). Key findings include a **2x revenue gap between male and female customers**, a subscription program that **isn't converting into higher per-customer spend**, and a loyal customer base that already accounts for the majority of the customer file — insights that translate directly into targeted, revenue-focused recommendations below.

## Business Problem

Retail teams collect enormous volumes of transaction data but often lack a structured way to turn it into decisions. This project simulates a real stakeholder request: **understand who is buying, what drives their spend, and where the business should focus retention and marketing dollars** — answered through a reproducible, three-stage analytics workflow rather than one-off spreadsheet analysis.

Core questions addressed:
- Who generates the most revenue, and by how much?
- Does the subscription program actually increase spend?
- Which products and customer segments deserve the most marketing/discount investment?
- What separates new, returning, and loyal customers?

## Methodology

**1. Data Cleaning & Feature Engineering (Python)**
- Imputed missing review ratings using the **category-level median** (chosen over mean to avoid distortion from outliers)
- Standardized all column names to lowercase with underscores for consistency and fewer downstream errors
- Cleaned and renamed fields (e.g., `purchase_amount_(usd)` → `purchase_amount`)
- Engineered an `age_group` feature using quantile-based binning (`qcut`) for equal-sized age segments
- Engineered `purchase_frequency_days` by mapping categorical purchase-frequency labels to numeric day values
- Validated data integrity by cross-checking promo code usage against the discount-applied flag

**2. Business Analysis (SQL / SQLite)**
- Connected the cleaned dataset to SQLite and wrote 10 business-question queries covering revenue by gender, discount behavior, shipping type, subscription economics, customer segmentation (CTEs), and top products per category (window functions with `ROW_NUMBER() OVER PARTITION BY`)

**3. Executive Dashboard (Power BI)**
- Built DAX measures for customer count, average purchase amount, and average review rating
- Designed an interactive dashboard with a subscription-status donut chart, category-level revenue and customer-count column charts, and an age-group revenue/sales bar chart
- Added slicers (subscription status, gender, category, shipping type) for real-time filtering by stakeholders

## Skills Demonstrated

**Technical:** Python (Pandas), SQL (CTEs, window functions, aggregate queries, SQLite), Power BI, DAX, Power Query
**Analytical:** data cleaning & imputation, feature engineering, customer segmentation, exploratory data analysis
**Business:** revenue analysis, customer lifecycle/retention analysis, dashboard storytelling for stakeholders

## Results & Business Recommendations

**Revenue Drivers**
- Male customers generated **$157,890** in revenue vs. **$75,191** from female customers — a **2.1x gap** out of $233,081 total
  → **Recommendation:** Investigate whether this reflects category mix or customer volume, and pilot a targeted campaign to grow female-segment revenue, since it currently represents just 32% of total sales.

**Subscription Program Is Not Paying Off in Spend**
- Non-subscribers (2,847 customers) generated **$170,436** in revenue at an average spend of **$59.87**
- Subscribers (1,053 customers) generated only **$62,645** at an average spend of **$59.49** — essentially identical per-customer spend
  → **Recommendation:** The subscription program isn't driving a spend premium. Re-evaluate its value proposition (e.g., exclusive discounts, early access) rather than assuming subscription status alone increases customer value.

**Untapped Conversion Opportunity**
- Of customers with **more than 5 previous purchases**, **2,518 are still not subscribed**, vs. only 958 who are
  → **Recommendation:** This is the highest-leverage conversion audience — proven repeat buyers who haven't joined the program. Target them directly rather than broad-based subscription marketing.

**Customer Base Is Already Loyalty-Heavy**
- Segmentation by previous purchases shows **3,116 "loyal" customers**, **701 "returning"**, and only **83 "new"**
  → **Recommendation:** Retention, not acquisition, should be the primary lever — protect the loyal base with proactive engagement, while separately investing in top-of-funnel efforts to rebuild the new-customer pipeline.

**Discount Strategy Needs a Margin Check**
- Hats, coats, and sneakers carry the highest discount rates (48–50% of purchases), yet don't appear among the top 5 highest-rated products
  → **Recommendation:** Audit margin impact on these high-discount items — heavy discounting isn't correlated with higher satisfaction, so it may be eroding margin without a loyalty payoff.

**Shipping & Age-Group Patterns**
- Express-shipping customers spend slightly more on average (**$60.48** vs. **$58.46** for Standard)
- Young Adults lead revenue by age group (**$62,143**), narrowly ahead of Middle Age ($59,197), Adult ($55,978), and Senior ($55,763)
  → **Recommendation:** Revenue is fairly evenly spread across age groups — age-based targeting has limited upside compared to the subscription and gender-gap opportunities above, which show far larger deltas.

---
*Dashboard built in Power BI with a Python → SQL → Power BI pipeline. Full query logic and Power BI build steps are documented alongside this README.*
