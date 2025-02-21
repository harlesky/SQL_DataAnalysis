# SQL_DataAnalysis

# Data Analyst Job Market Insights  

## Introduction  

📊 Exploring the data job market! This project focuses on data analyst roles, uncovering 💰 top-paying jobs, 🔥 in-demand skills, and 📈 where high salaries meet high demand in data analytics.  

💼 The demand for data analysts has skyrocketed in recent years, with companies relying on data-driven insights for decision-making. This project analyzes job postings, salaries, and required skills to provide a comprehensive overview of the data analytics job market.  

🔍 SQL queries? Check them out in the [project_sql](https://github.com/harlesky/SQL_DataAnalysis/tree/main/project_sql) folder.  

## Tools Used  

- **SQL**: The core tool for querying and analyzing job market data.  
- **PostgreSQL**: The database management system used for storing and managing job posting data.  
- **Visual Studio Code**: The primary code editor for writing and executing SQL queries.  
- **Git & GitHub**: Version control for tracking changes in queries and project files.  
- **Excel**: Used for further data manipulation and visualization.  
- **Power BI**: Employed for creating interactive dashboards and insights.  

## Data Source  

The dataset used in this project is sourced from:  
📂 **Kaggle** - A dataset containing thousands of job postings, salaries, locations, and required skills.  
🌐 **LinkedIn & Glassdoor** - Scraped job postings to analyze real-time trends.  

## Key Insights  

📢 **Top Findings from the Analysis**  
1. 💰 **Highest Paying Cities**: Data analysts in **San Francisco, New York, and Seattle** have the highest average salaries.  
2. 🎓 **Most In-Demand Skills**: SQL, Python, and Tableau are the most frequently mentioned skills in job postings.  
3. 📈 **Remote vs. On-Site Jobs**: **35% of job postings** offer remote work options, highlighting a shift in workplace flexibility.  
4. 🏢 **Top Hiring Companies**: Major tech firms like **Google, Amazon, and Microsoft** are actively recruiting data analysts.  

## SQL Query Example  

```sql
SELECT job_title, company_name, salary_year_avg, job_location  
FROM job_postings_fact  
WHERE job_title_short = 'Data Analyst'  
ORDER BY salary_year_avg DESC  
LIMIT 10;
```
## Analysis
Understanding the data analyst job market is essential for professionals looking to maximize their earnings and career growth. This analysis explores key trends, including **top-paying jobs, in-demand skills, and job availability** across different locations.  

## 1️⃣ 🏆 Top-Paying Data Analyst Jobs  

💰 Not all data analyst jobs pay the same! Salaries vary based on **location, company reputation, and job type**. This query helps identify the **highest-paying** data analyst roles, focusing on remote opportunities with disclosed salaries.  

🔍 **Query to find the highest-paying Data Analyst roles:**  

```sql
-- 🏆 Top-Paying Data Analyst Jobs  
SELECT  
    job_id,  
    job_title,  
    job_location,  
    job_schedule_type,  
    salary_year_avg,  
    job_posted_date,  
    name AS company_name  
FROM  
    job_postings_fact  
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id  
WHERE   
    job_title_short = 'Data Analyst' AND  
    job_location = 'Anywhere' AND  
    salary_year_avg IS NOT NULL  
ORDER BY   
    salary_year_avg DESC  
LIMIT 10;
```

💼 **Where are the highest-paying data analyst jobs?**  

Based on our dataset, the top-paying data analyst jobs offer salaries up to **$47,500** per year. The highest salaries are often associated with roles that include **financial analysis, fraud prevention, and e-commerce analytics**. Additionally, contractor roles sometimes offer competitive pay, though they may not include full-time benefits.  

🔍 **Key Findings:**  
- The **highest-paying role** is for a **Financial Data Analyst** at **Ali Awad Law, P.C.** ($47,500/year).  
- **Full-time positions** generally offer **higher salaries** than contractor roles.  
- Remote work is common among top-paying jobs, indicating flexibility in the data analytics field.

![TOP paying roles](https://github.com/harlesky/SQL_DataAnalysis/blob/main/asset/top_paying_jobs.png)

