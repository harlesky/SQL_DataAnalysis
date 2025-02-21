# SQL_DataAnalysis

Data Analyst Job Market Insights

Introduction

📊 Exploring the data job market! This project focuses on data analyst roles, uncovering 💰 top-paying jobs, 🔥 in-demand skills, and 📈 where high salaries meet high demand in the field of data analytics.

🔍 SQL queries? Check them out in the project_sql folder.

Background

This project was inspired by the need to better understand the data analyst job market—identifying top-paying roles and the most sought-after skills. The goal is to streamline job search efforts by highlighting key industry trends.

The dataset, sourced from an SQL course, provides insights into job titles, salaries, locations, and the essential skills required.

Key Questions Addressed

Which data analyst jobs offer the highest salaries?

What skills are required for these top-paying jobs?

Which skills are most in demand?

What skills are linked to higher salaries?

What are the best skills to learn for career growth?

Tools Used

To analyze the job market, the following tools were utilized:

SQL: The core tool for querying and analyzing job market data.

PostgreSQL: The database management system used to store and manage job postings.

Visual Studio Code: Used for database management and SQL query execution.

Git & GitHub: Used for version control and sharing SQL scripts.

Analysis

1. Top-Paying Data Analyst Jobs

To identify the highest-paying positions, job listings were filtered by average yearly salary, with a focus on remote opportunities.

SQL Query:

SELECT	
    job_id,
    job_title,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date,
    name AS company_name
FROM job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst'
    AND job_location = 'Anywhere'
    AND salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC
LIMIT 10;

Key Insights:

Salaries range from $184,000 to $650,000.

Employers include major companies like SmartAsset, Meta, and AT&T.

Job titles vary widely, from Data Analyst to Director of Analytics.

2. Skills for Top-Paying Jobs

To determine the most valuable skills, job postings were joined with skill data to uncover patterns.

SQL Query:

WITH top_paying_jobs AS (
    SELECT	
        job_id,
        job_title,
        salary_year_avg,
        name AS company_name
    FROM job_postings_fact
    LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
    WHERE
        job_title_short = 'Data Analyst'
        AND job_location = 'Anywhere'
        AND salary_year_avg IS NOT NULL
    ORDER BY salary_year_avg DESC
    LIMIT 10
)
SELECT
    top_paying_jobs.*,
    skills
FROM top_paying_jobs
INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY salary_year_avg DESC;

Key Insights:

SQL appears in 8 out of 10 top-paying jobs.

Python is a close second with 7 mentions.

Other highly valued skills include Tableau, R, Snowflake, and Excel.

3. Most In-Demand Skills

To uncover the most frequently requested skills, job postings were analyzed based on skill demand.

SQL Query:

SELECT
    skills,
    COUNT(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst'
    AND job_work_from_home = True
GROUP BY skills
ORDER BY demand_count DESC
LIMIT 5;

Key Insights:

Skill

Demand Count

SQL

7,291

Excel

4,611

Python

4,330

Tableau

3,745

Power BI

2,609

4. Skills Associated with Higher Salaries

Analyzing average salaries for different skills helped identify the most lucrative ones.

SQL Query:

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
GROUP BY skills
ORDER BY avg_salary DESC
LIMIT 10;

Key Insights:

Skill

Average Salary ($)

PySpark

208,172

Bitbucket

189,155

Couchbase

160,515

DataRobot

155,486

Jupyter

152,777

Pandas

151,821

5. Most Optimal Skills to Learn

By combining demand and salary data, skills that offer the best career opportunities were identified.

SQL Query:

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
GROUP BY skills_dim.skill_id
HAVING COUNT(skills_job_dim.job_id) > 10
ORDER BY avg_salary DESC, demand_count DESC
LIMIT 10;

Key Insights:

Skill

Demand Count

Average Salary ($)

Go

27

115,320

Confluence

11

114,210

Hadoop

22

113,193

Snowflake

37

112,948

Azure

34

111,225

Key Takeaways

🧩 Advanced SQL Skills: Gained experience with complex queries, joins, and temp tables.

📊 Data Aggregation: Mastered using GROUP BY, COUNT(), and AVG() to extract meaningful insights.

🚀 Market Trends: Learned which skills are highly valued and how they affect salary potential.

This project provides actionable insights for those entering or advancing in the data analytics field. If you're looking to maximize job prospects and salary potential, focusing on high-demand and well-paid skills is key!

📂 Check out the SQL queries in the project_sql folder!

