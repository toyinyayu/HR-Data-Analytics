# HR-Data-Analytics - Home

## Table of Content

- [Project Overview](#project-overview)
- [Data Analysis](#data-analysis)
- [Recommendation](#recommendation)

### Project Overview
This project shows the Analysis for an HR Department, showing relevant KPIs to show Employee Performance and Job Satisfaction and also help the organization to improve on their people skills and recruitment process.
![HR Data CCG_page-0001](https://github.com/toyinyayu/HR-Data-Analytics/assets/31111105/4114cb97-eb46-4b3b-ac9c-cec69f2790ca)


### Data Source
HR Data - The primary dataset used for this analysis is "hr_analytics_data.csv" file, containing detail information about each employee and their productivity level in the company.

### Tools
- Excel - Data Cleaning
- PowerBI - Creating Report and Visuals
- SQL Server - Data Analysis


### Data Cleaning and Tranformation
In the initial data preparation phase, I performed the following task:
1. Data loading and Inspection.
2. Handling Missing Values
3. Data Cleaning and formatting

### Exploratory Data Analysis (EDA)
EDA involved exploring Employee Data to answer questions, such as:

- What is the total number of Employee?
- What is the gender based percentage of Employee?
- How many employee is due for Promotion and Retrenchment?
- How many active workers?
- What is the job level and satisfaction of each Employee?


### Data Analysis

```SQL
#### Total Count of Employee
SELECT COUNT(EmployeeCount)
FROM 
	hr_mgt.dbo.hr_analytics_data;
```

### Percentage of Employee Gender by Male & Female

```SQL
 SELECT (Gender), 
  COUNT(*) As Gender_Type,
  CONCAT(ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER (), 2), '%') AS Percentage
  FROM [hr_mgt].[dbo].[hr_analytics_data]
  GROUP BY (Gender)
```

### Numbers of Employee Due for Promotion

```SQL
 SELECT
   Count(Due_for_promotion) AS Empoyee_Due_For_Promotion
  FROM 
	hr_mgt.dbo.data_promomtion;
```

### Changing my Datatypes

```SQL
	ALTER TABLE hr_mgt.dbo.data_retrenchment
	ALTER COLUMN retrenched TINYINT;
```

### Total Number of Employee Due for Retrenchment and Active Workers 

```SQL 
SELECT 
	SUM(retrenched) AS Employee_Due_For_Retrenchment,
	COUNT(CASE WHEN retrenched = 0 OR retrenched IS NULL THEN 1 ELSE NULL END) AS Active_Workers
	FROM
	hr_mgt.dbo.data_retrenchment;
```

### Total Count of Employee By Job Level in 5 Different Level

```SQL
SELECT
    JobLevel,
    COUNT(*) AS Level_Count
FROM (
    SELECT
        JobLevel AS Filled_Number,
        CASE
            WHEN JobLevel = 1 THEN 'Level 1'
            WHEN JobLevel = 2 THEN 'Level 2'
            WHEN JobLevel = 3 THEN 'Level 3'
            WHEN JobLevel = 4 THEN 'Level 4'
            WHEN JobLevel = 5 THEN 'Level 5'
            
        END AS JobLevel
    FROM
        hr_mgt.dbo.hr_analytics_data
) AS Subquery
GROUP BY
    JobLevel
ORDER BY
	JobLevel ASC;

```

### Total Years Spent By Employee in Ranges 

```SQL
SELECT
    TotalWorkingYears,
    COUNT(*) AS Years_Spent
FROM (
    SELECT
        TotalWorkingYears AS Filled_Number,
        CASE
            WHEN TotalWorkingYears BETWEEN 0 AND 5 THEN '0-5years'
            WHEN TotalWorkingYears BETWEEN 5 AND 10 THEN '6-10years'
            WHEN TotalWorkingYears BETWEEN 11 AND 15 THEN '11-15years'
            WHEN TotalWorkingYears BETWEEN 16 AND 20 THEN '16-20years'
            WHEN TotalWorkingYears BETWEEN 21 AND 25 THEN '21-25years'
			WHEN TotalWorkingYears BETWEEN 26 AND 30 THEN '26-30years'
			WHEN TotalWorkingYears BETWEEN 31 AND 35 THEN '31-35years'
			WHEN TotalWorkingYears BETWEEN 36 AND 40 THEN '36years Above'

   
        END AS TotalWorkingYears
    FROM
        hr_mgt.dbo.hr_analytics_data
) AS Subquery
GROUP BY
    TotalWorkingYears
ORDER BY
	TotalWorkingYears ASC;
```

### Employee Based on Distance from Work

```SQL
SELECT
    DistanceFromHome,
    COUNT(*) AS Years_Spent
	
	
FROM (
    SELECT
        DistanceFromHome AS Filled_Number,
        CASE
            WHEN DistanceFromHome BETWEEN 0 AND 9 THEN 'Very close'
            WHEN DistanceFromHome BETWEEN 10 AND 19 THEN 'Close'
            WHEN DistanceFromHome BETWEEN 20 AND 30 THEN 'Very Far'
          
        END AS DistanceFromHome
    FROM
        hr_mgt.dbo.hr_analytics_data
) AS Subquery
GROUP BY
    DistanceFromHome
ORDER BY
	DistanceFromHome ASC;
```





