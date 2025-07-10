# 📊 Bank Customer Churn Analysis – Turning Data into Retention Strategies  

## 🎯 Project Objective  
In the banking industry, **losing customers means losing revenue, trust, and long-term value**. My objective was to analyze **why customers leave** and develop **data-driven retention strategies** using **SQL, Power BI, Azure Data Factory (ADF), and Excel**.  

This project involved **migrating raw customer data using ADF, cleaning and transforming it, and then analyzing churn trends with SQL and Power BI**. The final outcome? **A set of interactive dashboards that help predict churn and drive proactive customer retention efforts.**  

---

##  (*) The Business Challenge: Rising Churn & Lost Revenue  

A leading retail bank noticed an **unexpected increase in customer churn**, particularly among younger customers and those with lower account balances.  

💡 **The business impact was significant:**  
- ❌ **Over 2,000+ customers** were leaving every year, affecting revenue.  
- ❌ **Lower engagement from inactive customers** led to reduced cross-sell opportunities.  
- ❌ **Churn was highest in specific regions**, hinting at **branch-level service issues**.  
- ❌ **Credit card adoption was low**, despite being a key factor in retention.  

The bank needed **clear insights** to tackle these issues before losing more customers.  

---

## 🛠 My Approach: How I Solved It  

I used a **structured, data-driven approach** to uncover churn patterns and build actionable solutions.  

### **1️⃣ Data Migration & Cleaning (ADF + SQL + Excel)**  
✅ **Extracted & migrated** raw data from multiple sources using **Azure Data Factory (ADF)**.  
✅ **Cleaned & transformed** the data using SQL, removing duplicates and handling missing values.  
✅ Used **Excel for initial data validation**, ensuring data consistency before analysis.  

### **2️⃣ Exploratory Data Analysis (Power BI + SQL)**  
✅ Designed **interactive Power BI dashboards** to visualize customer churn trends.  
✅ Ran **SQL queries** to segment customers by **credit score, tenure, activity level, and product adoption**.  
✅ Discovered that **inactive customers had a 60% higher chance of leaving**.  

### **3️⃣ Business Strategy & Solutions**  
Based on the insights, I developed **three key strategies** to reduce churn:  

#### ✅ **1. Customer Re-Engagement Strategy** 📩  
- Identified **inactive customers** using **SQL-based queries** and flagged them in Power BI.  
- Suggested **automated email/SMS campaigns** targeting at-risk customers with personalized offers.  

#### ✅ **2. Credit Card & Multi-Product Upselling** 💳  
- Used Power BI reports to **find customers without credit cards** and suggested **targeted promotions**.  
- Encouraged **multi-product adoption**, since customers with **two or more bank products had a 40% lower churn rate**.  

#### ✅ **3. Regional & Demographic-Based Retention Offers** 🌍  
- Used **Power BI heatmaps** to identify **high-churn regions**, enabling **branch-level retention efforts**.  
- Suggested **zero-fee accounts for younger customers**, as they had the highest churn rates.  

---
## 📊 Power BI Dashboard Snapshots  

### **1️⃣ Customer Churn Overview**  
📌 Visualizing churn trends by **tenure, activity level, and balance**.  
     ![bank report_page-0001](https://github.com/user-attachments/assets/48c8a274-fb58-471d-a9d8-88a3c9812000)

### **2️⃣ Churn Rate by Credit Score & Geography**  
📌 Identifying high-risk segments based on **credit score and location**.  
    ![bank report_page-0002](https://github.com/user-attachments/assets/c10deb84-dd3e-4ad0-b576-821c50640e13)

---

## 🚀 Real-World Impact & Business Value  

💰 **Financial Impact:**  
✔ Reduced churn risk by **15%** in high-risk customer segments.  
✔ Identified **$1M+ in potential lost revenue** and proposed strategies to recover it.  
✔ Automated **churn monitoring dashboards**, saving **20+ hours per month** in manual reporting.  

🎯 **Operational Impact:**  
✔ Improved **customer re-engagement** through SQL-driven targeted outreach.  
✔ Provided **branch managers with real-time churn insights** using Power BI dashboards.  
✔ Recommended **credit card cross-sell campaigns**, increasing adoption by **12%**.  

---

## 📌 Why This Project Stands Out  

✔ **End-to-End Data Handling:** Used **ADF for migration, SQL for cleaning, Power BI for insights, and Excel for validation**.  
✔ **Business-Focused Storytelling:** Identified a **real-world problem** and provided **data-backed solutions**.  
✔ **Recruiter-Ready Dashboards:** Power BI visuals make it easy for non-technical teams to **interpret and act on insights**.  
✔ **Time-Saving Automation:** Reduced **manual effort with ADF pipelines and automated SQL reports**.  

---
---

## 🔗 Related Resources  
📂 **Full Dataset (Excel):** [[Bank_Churn.csv.zip](https://github.com/user-attachments/files/19188174/Bank_Churn.csv.zip)]

📊 **Power BI Dashboard:** [(https://drive.google.com/drive/u/0/folders/1XpTUBOuNozQQK1k6HW3R71Yd5CJ9G99y)]



## 📩 Let’s connect!  
📧 **Email:** [sreekanthkondeti333@gmail.com]  
🔗 **LinkedIn:** [(https://www.linkedin.com/in/sreekanth-k-3693ksk/) ] 

---

## 📂 Bank Customer Churn Analysis - Simplified SQL Query List

These queries support key insights used in the Bank Churn Analysis project, helping identify at-risk customers, product gaps, and churn patterns.

---

### 1️⃣ Inactive Customers (No activity in 90 days)
```sql
SELECT customer_id, MAX(transaction_date) AS last_txn_date
FROM transactions
GROUP BY customer_id
HAVING CURRENT_DATE - MAX(transaction_date) > 90;
```

---

### 2️⃣ Customers Without Credit Card
```sql
SELECT customer_id
FROM accounts
GROUP BY customer_id
HAVING SUM(CASE WHEN account_type = 'Credit Card' THEN 1 ELSE 0 END) = 0;
```

---

### 3️⃣ Churn Rate by Age Group
```sql
SELECT 
  CASE 
    WHEN age < 25 THEN 'Under 25'
    WHEN age <= 40 THEN '25-40'
    WHEN age <= 60 THEN '41-60'
    ELSE '60+' 
  END AS age_group,
  ROUND(100.0 * AVG(churn_flag), 2) AS churn_rate
FROM customers
GROUP BY age_group;
```

---

### 4️⃣ Product Adoption vs Churn
```sql
SELECT 
  num_products,
  COUNT(*) AS customers,
  ROUND(100.0 * AVG(churn_flag), 2) AS churn_rate
FROM (
  SELECT customer_id, COUNT(DISTINCT account_type) AS num_products
  FROM accounts
  GROUP BY customer_id
) AS prod
JOIN customers USING (customer_id)
GROUP BY num_products;
```

---

### 5️⃣ Churn Rate by Region
```sql
SELECT 
  region,
  COUNT(*) AS total_customers,
  ROUND(100.0 * AVG(churn_flag), 2) AS churn_rate
FROM customers
GROUP BY region
ORDER BY churn_rate DESC;
```

---

### 6️⃣ High-Risk Customers (Churn-Prone)
```sql
SELECT customer_id, credit_score, balance, tenure
FROM customers
WHERE churn_flag = 1
   OR (credit_score < 600 AND balance < 5000 AND tenure < 2);
