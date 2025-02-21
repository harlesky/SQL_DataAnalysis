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

![TOP paying roles](https://github.com/harlesky/SQL_DataAnalysis/blob/main/asset/top_paying_data_analyst_jobs.png)
*Bar graph visualizing the salary for the top 10 salaries for data analysts; ChatGPT generated this graph from my SQL query results*

### 2. Skills for Top Paying Jobs
To understand what skills are required for the top-paying jobs, I joined the job postings with the skills data, providing insights into what employers value for high-compensation roles.
```sql
WITH top_paying_jobs AS (
    SELECT	
        job_id,
        job_title,
        salary_year_avg,
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
    LIMIT 10
)

SELECT 
    top_paying_jobs.*,
    skills
FROM top_paying_jobs
INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY
    salary_year_avg DESC;
```
The breakdown of the most demanded skills for the top 10 highest-paying data analyst jobs in 2023:
- **SQL** is leading with a bold count of 8.
- **Python** follows closely with a bold count of 7.
- **Tableau** is also highly sought after, with a bold count of 6.
Other skills like **R**, **Snowflake**, **Pandas**, and **Excel** show varying degrees of demand.

![Top Paying Skills](https://github.com/harlesky/SQL_DataAnalysis/blob/main/asset/2_top_paying_roles_skills.png)
*Bar graph visualizing the count of skills for the top 10 paying jobs for data analysts; ChatGPT generated this graph from my SQL query results*

### 3. In-Demand Skills for Data Analysts

This query helped identify the skills most frequently requested in job postings, directing focus to areas with high demand.

```sql
SELECT 
    skills,
    COUNT(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst' 
    AND job_work_from_home = True 
GROUP BY
    skills
ORDER BY
    demand_count DESC
LIMIT 5;
```
Here's the breakdown of the most demanded skills for data analysts in 2023
- **SQL** and **Excel** remain fundamental, emphasizing the need for strong foundational skills in data processing and spreadsheet manipulation.
- **Programming** and **Visualization Tools** like **Python**, **Tableau**, and **Power BI** are essential, pointing towards the increasing importance of technical skills in data storytelling and decision support.

| Skills   | Demand Count |
|----------|--------------|
| SQL      | 7291         |
| Excel    | 4611         |
| Python   | 4330         |
| Tableau  | 3745         |
| Power BI | 2609         |

*Table of the demand for the top 5 skills in data analyst job postings*

### 4. Skills Based on Salary
Exploring the average salaries associated with different skills revealed which skills are the highest paying.
```sql
SELECT 
    skills,
    ROUND(AVG(salary_year_avg), 0) AS avg_salary
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst'
    AND salary_year_avg IS NOT NULL
    AND job_work_from_home = True 
GROUP BY
    skills
ORDER BY
    avg_salary DESC
LIMIT 25;
```
Here's a breakdown of the results for top paying skills for Data Analysts:
- **Strong Demand for Big Data & ML Expertise:** Analysts proficient in big data technologies (PySpark, Couchbase), machine learning tools (DataRobot, Jupyter), and Python libraries (Pandas, NumPy) earn top salaries, highlighting the industry's emphasis on data processing and predictive modeling.
- **Software Development & Deployment Proficiency:** Expertise in development and deployment tools (GitLab, Kubernetes, Airflow) bridges the gap between data analysis and engineering, with high value placed on automation and streamlined data pipeline management.
- **Cloud Computing Expertise:** Mastery of cloud and data engineering tools (Elasticsearch, Databricks, GCP) reflects the rising significance of cloud-based analytics, demonstrating that cloud expertise enhances earning potential in data analytics.

| Skills        | Average Salary ($) |
|---------------|-------------------:|
| pyspark       |            208,172 |
| bitbucket     |            189,155 |
| couchbase     |            160,515 |
| watson        |            160,515 |
| datarobot     |            155,486 |
| gitlab        |            154,500 |
| swift         |            153,750 |
| jupyter       |            152,777 |
| pandas        |            151,821 |
| elasticsearch |            145,000 |

*Table of the average salary for the top 10 paying skills for data analysts*

### 5. Most Optimal Skills to Learn

Combining insights from demand and salary data, this query aimed to pinpoint skills that are both in high demand and have high salaries, offering a strategic focus for skill development.

```sql
SELECT 
    skills_dim.skill_id,
    skills_dim.skills,
    COUNT(skills_job_dim.job_id) AS demand_count,
    ROUND(AVG(job_postings_fact.salary_year_avg), 0) AS avg_salary
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst'
    AND salary_year_avg IS NOT NULL
    AND job_work_from_home = True 
GROUP BY
    skills_dim.skill_id
HAVING
    COUNT(skills_job_dim.job_id) > 10
ORDER BY
    avg_salary DESC,
    demand_count DESC
LIMIT 25;
```

| Skill ID | Skills     | Demand Count | Average Salary ($) |
|----------|------------|--------------|-------------------:|
| 8        | go         | 27           |            115,320 |
| 234      | confluence | 11           |            114,210 |
| 97       | hadoop     | 22           |            113,193 |
| 80       | snowflake  | 37           |            112,948 |
| 74       | azure      | 34           |            111,225 |
| 77       | bigquery   | 13           |            109,654 |
| 76       | aws        | 32           |            108,317 |
| 4        | java       | 17           |            106,906 |
| 194      | ssis       | 12           |            106,683 |
| 233      | jira       | 20           |            104,918 |

*Table of the most optimal skills for data analyst sorted by salary*

Here's a breakdown of the most optimal skills for Data Analysts in 2023: 
- **High-Demand Programming Languages:** Python and R remain highly sought after, with demand counts of 236 and 148, respectively. Despite their popularity, their average salaries—$101,397 for Python and $100,499 for R—suggest that while these skills are valuable, they are also widely available.
- **Cloud Tools and Technologies:** Expertise in specialized platforms like Snowflake, Azure, AWS, and BigQuery commands strong demand and competitive salaries, emphasizing the increasing role of cloud computing and big data in data analytics.
- **Business Intelligence and Visualization Tools:** Tableau and Looker, with demand counts of 230 and 49, respectively, and average salaries of $99,288 and $103,795, underscore the essential role of data visualization and business intelligence in extracting actionable insights.
- **Database Technologies:**Proficiency in both traditional and NoSQL databases (Oracle, SQL Server, NoSQL) remains crucial, with average salaries ranging from $97,786 to $104,534, reflecting the continued importance of data storage, retrieval, and management.

# What I Learned

Throughout this adventure, I've turbocharged my SQL toolkit with some serious firepower:

- **🧩Advanced Query Crafting:**Mastered complex SQL queries, seamlessly joining tables and leveraging WITH clauses for efficient temporary table operations.
- **📊 Data Aggregation:** Became proficient in GROUP BY, making aggregate functions like COUNT() and AVG() my go-to tools for summarizing data.
- **💡 Analytical Wizardry:** Enhanced my ability to transform real-world questions into actionable, insight-driven SQL queries.

# Conclusions

### Insights
From the analysis, several general insights emerged:

1. **Top-Paying Data Analyst Jobs**:Remote data analyst roles can offer salaries as high as $650,000, showcasing the lucrative potential in the field.
2. **Skills for Top-Paying Jobs**:Advanced SQL proficiency is a common requirement for top-paying data analyst jobs, reinforcing its importance for career growth.
3. **Most In-Demand Skills**: SQL is also the most demanded skill in the data analyst job market, thus making it essential for job seekers.
4. **Skills with Higher Salaries**: Specialized skills, such as SVN and Solidity, are associated with the highest average salaries, indicating a premium on niche expertise.
5. **Optimal Skills for Job Market Value**: SQL leads in demand and offers for a high average salary, positioning it as one of the most optimal skills for data analysts to learn to maximize their market value.
