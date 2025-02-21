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


