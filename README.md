# Introduction
Explore the tech job market with an emphasis on data analytic roles. This project will give insights into top-paying jobs, high-demand skills, and demand to salary ratio.

SQL queries here: [project_sql folder](/project_sql/)

# Background
The goal of the project was to learn the basics of SQL and explore the data analytic field. This project was apart of a introduction course desigend and created by Luke Barousse.

Here is a link to Luke's [SQL Course](https://www.lukebarousse.com/sql)

### Questions to Answer
1. What are the top-paying jobs for data analytics?
2. What are the skills required for these top-paying roles?
3. What are the most in-demand skills for data analytics?
4. What are the top skills based on salary for data analytics?
5. What are the most optimal skills to learn?

     a. Optimal: High Demand AND High Paying

# Tools I Used
For this project I used several different tools:
- **SQL**: The main driver in driver for this project that allowed me to analyze the tech job market.
- **PostgreSQL**: A database management for all the job data.
- **Visual Studio Code**: Database management and exucuting SQL queires.
- **Git & GitHub**: Allowed me to share and document my jounrey as I learn the navigate the field of data analytics.
# The Analyssis
Each of the uploaded queries were implemeted to answer specific questions regarding the data analytic job market. 

### 1. Top Paying Data Analyst Jobs
To identify the top paying positions, I filtered the database by average salary along with the title of "Data Analyst" Here is the query that returned the those results.

```sql
SELECT
    job_id,
    company_dim.name AS company_name,
    job_title,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date
FROM 
    job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE
    salary_year_avg IS NOT NULL AND 
    job_title_short = 'Data Analyst' AND
    job_location = 'Anywhere'
ORDER BY
    salary_year_avg DESC
LIMIT 10
```
### Insert Visual Here ###

Here are some of findings for top data analyst roles in 2023:
- **Large Salary Range:** The top 10 roles have salaries that range from $184,000 to $650,000 which presents a vast salary range in the field.
- **Diverse Employers:** Numerious companies such as Mantys, Meta, AT&T, and others, shows a broad range of intrest for data anlayst roles.
- **Job Title Variety:** There are different roles in the field with jobs titles from Data Analyst to Director of Data Analytics revealing that there are many different specialties and directions. 

### 2. Skills for Top Paying Roles
To aquire the listed skills associated with the highest salaries, I joined two tables to select the skills. This was then ordered by highest salary. Here is the query that reflects it:

```sql
WITH top_paying_jobs AS (
    SELECT
        job_id,
        company_dim.name AS company_name,
        job_title,
        salary_year_avg
    FROM 
        job_postings_fact
    LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
    WHERE
        salary_year_avg IS NOT NULL AND 
        job_title_short = 'Data Analyst' AND
        job_location = 'Anywhere'
    ORDER BY
        salary_year_avg DESC
    LIMIT 10
)
SELECT 
    top_paying_jobs.*,
    skills_dim.skills
FROM 
    top_paying_jobs
INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY
    salary_year_avg DESC
```
### Insert Visual Here ###

Here are some findings for top paying skills:

- **Skill Frequency:** There are many different skills listed for top paying jobs. The most in-demand are SQL and Python
- **Skill Groups** It is not uncommon to see top paying jobs have multiple different skills listed
- ** 

### 3. What are the Most In-Demand Skills for Data Analytics?
The query below reflects how to filter data analyst jobs by grouping skills and then counting the amount of times a skill was listed.

```sql
SELECT
    skills,
    COUNT(skills_job_dim.job_id) AS demand_count
FROM job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst'
GROUP BY
    skills
ORDER BY
    demand_count DESC
LIMIT 5
```
### Insert Visual Here ###

Here are some of the findings from this

- **Top Skills:** SQL is highest in demand followed by Excel
- **Complementary Skills:** The list includes common skills that complement each other such as SQL for managiing databases and then using Power BI for visualzation.

### 4. What are the top skills based on salary for data analytics?



### 5. What are the most optimal skills to learn?
#### a. Optimal: High Demand AND High Paying




# Conclusions


