# Customer Churn Analysis – BankChurners Dashboard

**Power BI Dashboard | Data Source: BankChurners.csv | 10,127 customers**

## 🎯 Overview
- This dashboard analyzes the behavior and characteristics of credit card customers to identify the factors leading to customer churn.
- Based on the analysis results, the dashboard proposes suitable retention strategies for each customer segment.
- The entire pipeline includes: data processing and cleaning in Power Query, metric calculation with DAX, customer segmentation according to the RFM model, and result visualization on Power BI Desktop.

##  🚀 Objectives
- Determine the churn rate and trend within the total customer base.
- Explore behavioral and financial factors highly correlated with churn.
- Segment customers based on the RFM (Recency - Frequency - Monetary) model.
- Propose specific retention action plans for each customer segment.

## 📊 Data Description
- **File:** BankChurners.csv
- **Number of rows:** 10,127 customers
- **Source:** Kaggle
- **Dataset:** Credit Card Customers Dataset

### Original Columns

| Column | Description |
| ------ | ------ |
| CLIENTNUM | Customer identifier |
| Attrition_Flag | Status: Existing Customer/Attrited Customer |
| Customer_Age | Age (26-73, average 46.3) |
| Gender | Gender (M/F) |
| Dependent_count | Number of dependents (0-5) |
| Education_Level | Education level (7 levels) |
| Marital_Status | Marital status |
| Income_Category | Income group (<$40K - $120K+) |
| Card_Category | Card type: Blue / Silver / Gold / Platinum |
| Months_on_book | Number of months as a customer |
| Total_Relationship_Count | Number of products in use |
| Months_Inactive_12_mon | Number of inactive months (last 12 months) |
| Contacts_Count_12_mon | Number of bank contacts (last 12 months) |
| Credit_Limit | Credit limit |
| Total_Revolving_Bal | Revolving balance |
| Total_Trans_Amt | Total transaction amount (12 months) |
| Total_Trans_Ct | Total transaction count (12 months) |
| Total_Amt_Chng_Q4_Q1 | Change in transaction amount Q4 vs Q1 |
| Total_Ct_Chng_Q4_Q1 | Change in transaction count Q4 vs Q1 |
| Avg_Utilization_Ratio | Average credit limit utilization ratio |

### Additional Columns & Tables Created in Power BI

| Column / Table | Description |
| ------ | ------ |
| Attrition_Flag_Bool | Binary conversion: 1 = churn, 0 = retained |
| Total_Trans_Amt_Rank | Transaction amount ranking |
| Recency | R score in the RFM model |
| Frequency | F score in the RFM model |
| Monetary | M score in the RFM model |
| RFM | Composite RFM score |
| Encoded_Education_Level | Encoded education level (0-6) |
| Customer_Segment | Segment: Loyal Customer / Middle / High Risk |
| Melt table | Long format (unpivot): attribute, value, Attrition_Flag, Clientnum |
| FRM table | Summary: RFM band, churn_rate, num_users |

### Measures (DAX)
- Attrited Rate, IQR, Q1, Q3, Lower (IQR lower bound), Upper (IQR upper bound)

---

## 📈 Key Analysis Results

### Churn Overview
| Metric | Value |
| ------ | ------ |
| Total customers | 10,127 |
| Churned customers | 1,627 |
| Retained customers | 8,500 |
| Overall churn rate | 16.07% |

### Transaction Behavior – Difference Between the 2 Groups
| Metric | Churned Customers | Retained Customers | Difference |
| ------ | ------ | ------ | ------ |
| Total transaction amount | $3,095 | $4,655 | ▼ 33% |
| Transaction count | 44.9 times | 68.7 times | ▼ 35% |
| Inactive months | 2.69 months | 2.27 months | ▲ 0.42 months |
| Bank contacts | 2.97 times | 2.36 times | ▲ 26% |
| Number of products in use | 3.28 | 3.91 | ▼ 16% |
| Limit utilization ratio | 16.2% | 29.6% | ▼ 13.4% |
| Credit limit | $8,136 | $8,727 | ▼ 7% |
| Change in transaction count Q4/Q1 | 0.554 | 0.742 | ▼ 25% |

- **Remarks:** The sharp decline in transaction count and transaction amount is the clearest early warning signal.
- Customers begin to reduce card usage before officially churning.

### Churn Rate by Demographics

**By Card Type:**

| Card Type | Number of Customers | Churn Rate |
| :--- | :--- | :--- |
| Blue | 9,436 | 16.1% |
| Silver | 555 | 14.77% |
| Gold | 116 | 18.1% |
| Platinum | 20 | 25.0% |

**By Income:**

| Income Group | Number of Customers | Churn Rate |
| :--- | :--- | :--- |
| Less than $40K | 3,561 | 17.19% |
| $40K-$60K | 1,790 | 15.14% |
| $60K-$80K | 1,402 | 13.48% |
| $80K-$120K | 1,535 | 15.77% |
| $120K+ | 727 | 17.33% |

- **Remarks:** The lowest income group (<$40K) and the highest income group ($120K+) both have the highest churn rates, indicating that the issue lies in product suitability, not merely financial capacity.

**By Gender:**

| Gender | Number of Customers | Churn Rate |
| :--- | :--- | :--- |
| Female (F) | 5,358 | 17.36% |
| Male (M) | 4,769 | 14.62% |

---

## 👥 Customer Segmentation
Segmentation is built based on the RFM (Recency - Frequency - Monetary) score, combined with Months_Inactive_12_mon and Total_Trans_Amt_Rank.

| Segment | Number of Customers | % of Total | Churn Rate | Key Characteristics |
| ------ | ------ | ------ | ------ | ------ |
| Loyal Customer | 3,695 | 36.49% | 1.95% Low | Frequent transactions, multiple products in use, few inactive months |
| Middle | 2,930 | 28.93% | 15.6% Medium | Moderate transactions, signs of decreasing usage frequency |
| High Risk | 3,502 | 34.58% | 31.15% High | Few transactions, many inactive months, few products, low RFM score |

- The High Risk segment accounts for nearly 35% of the customer base – this is the priority group for intervention.

---

## Recommendations & Action Plan

### High Risk – Urgent Intervention
- **Signs:** Low RFM score (band 1-2), transaction count under 45/year, inactive for 2 or more months.
- **Actions:**
  - Set up automated alerts when customers reach the 2-month inactivity threshold.
  - Proactively contact (personalized call or email) within 7 days.
  - Provide instant incentives: annual fee waiver, transaction cashback, or credit limit upgrade.
  - Assign Relationship Managers (RM) to directly monitor the high-value Blue card group.
- **Goal:** Reduce the churn rate of this group to below 25%.

### Middle – Increase Engagement & Cross-sell
- **Signs:** Medium RFM score (band 3-4), using 1-2 products, transaction frequency decreasing compared to the previous period (low Q4/Q1).
- **Actions:**
  - Recommend a suitable second product (savings account, consumer loan, insurance).
  - Send personalized notifications after 30 days without new transactions.
  - Offer a point accumulation or cashback program upon reaching a monthly transaction threshold.
  - Organize annual credit limit reviews to create a sense of recognition.
- **Goal:** Increase the ownership rate of 2+ products from approximately 48% to 65%.

### Loyal Customer – Maintain & Develop
- **Signs:** High RFM score (band 5), regular transactions, using multiple products, good utilization ratio.
- **Actions:**
  - Build a clear card upgrade path (Blue -> Silver -> Gold -> Platinum).
  - Implement an attractive referral program to expand the customer base.
  - Send personalized annual reports (summary of targets, reward points, utilized benefits).
  - Prioritize preferential support when this group shows signs of abnormal transaction reduction.
- **Goal:** Maintain the churn rate below 5% and increase revenue from this group through upsell.

---

## 🌟 General Findings That Require Continuous Monitoring
| Warning Signal | Proposed Intervention Threshold |
| ------ | ------ |
| Decrease in transaction count | Under 45 times/year |
| Inactive months | 2 months or more |
| Limit utilization ratio | Under 10% |
| Owning only 1 product | Prioritize cross-selling immediately |
| Number of bank contacts | 4 times or more (signs of complaints) |

---

## 🛠 Tools Used
- **Power BI Desktop:** Visualization and interaction.
- **Power Query (M):** Data cleaning, transformation, and group column creation.
- **DAX:** Dynamic metric calculation (Attrited Rate, RFM, IQR, Q1, Q3, Lower, Upper).
- **Excel & CSV:** Data cleaning and initial processing.
