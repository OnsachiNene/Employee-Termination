# Welcome to my Employee Termination Exploratory Analysis! Stay with me as we uncover the secrets of this dataset

### This Project is all about:
- Cleaning and Norminalizing jumbled datasets
- Perfoming CRUD operations to answer burning questions
- Putting all of this information in a picture, i mean, its worth more than a thousand words anyway.
  
### Data Source
#### On a very sunny day while i was lazying away, my friend, Ben (Pseudo name) sent me this dataset, ill ask her where exactly she got it from. The data set is saved as "Try this. csv". It contains information about the employees, you know, regular stuff, Id, department and so on, as well as their hire and termination dates.

### Tools used
- Excel (Power Query: Missing Value Handling, Data Type Fixes)
- SQL (Filtering, Aggregation, Data Integrity Checks)
- Azure Data Studio (Bar Charts, Attrition Visuals)

### Let’s dive into the queries and uncover the story hidden in the data
#### Data Cleaning and Preparation
The dataset was first loaded into Excel for an initial inspection. Using Power Query, I cleaned and transformed the data—this included changing data types, replacing inconsistent values, and handling missing entries.
Next, I imported the cleaned data into SQL, where I performed CRUD operations to explore the dataset. I used (SELECT), (COUNT), (AGGREGATE), and (FILTER) functions to answer specific questions. Data cleaning continued within SQL as well—because let’s be honest, data cleaning is never really one and done

### Exploratory Analysis. 
- For this dataset, I set out to answer the following key questions:
1. Which department has the highest attrition rate?
2. Which location—Headquarters or Remote—experiences more employee turnover?
3. Which age group records the highest rate of attrition?
4. These questions guided my analysis and helped uncover patterns that could inform better HR decision-making.



### 🧮 SQL Magic 
#### Before diving into deeper analysis, I wanted to ensure data integrity by checking for any duplicates. Verifying the uniqueness of employee records is crucial to avoid skewed insights and ensure accurate results
```sql
--This checks if an employee is in more than one department
SELECT id, COUNT (Department) AS Count_Dep 
  FROM Att 
  WHERE Term_date IS NOT NULL
  GROUP BY id 
  HAVING COUNT (Department) >1
```
```sql
--This checks if there are duplicated ids
SELECT id, COUNT(id) AS Count_id
FROM Att
WHERE Count_id IS NOT NULL
GROUP BY id
HAVING COUNT(id) > 1
```
### Question 1- What department has the highest staff attrition?
```sql
SELECT Department, COUNT (Department) as Count 
  FROM Att 
  WHERE Term_date IS NOT NULL 
  GROUP BY Department 
  ORDER BY Count DESC
```
![Dep 2](https://github.com/user-attachments/assets/8af95fc2-345d-4f79-a990-21e2cd7bd198)

#### The highest attrition rate was in the Engineering department, suggesting possible burnout or dissatisfaction that may require HR intervention.

### Question 2- What Location (Head quarter or Remote) has the highest attrition?
```sql
SELECT Location, COUNT (Location)How_many 
  FROM Att 
  WHERE Term_date IS NOT NULL 
  GROUP BY Location 
  ORDER BY How_many DESC
```
 ![location](https://github.com/user-attachments/assets/7ab2175b-2422-4e2a-9d46-d6fd09e21414)
#### Results show that the highest attrition rates are from the headquarters. This suggests possible workplace-related challenges such as increased pressure, stricter supervision, lack of flexibility, or lower job satisfaction compared to remote workers. It may indicate the need for HR to further investigate internal policies, management styles, or employee engagement strategies at the headquarters to improve retention

### Question 3- What age group has the highest attrition?
- The original table does not have an Age group column, which necessitated the need to use subqueries
```sql
SELECT 
    Age_group, 
    COUNT(*) AS How_many
FROM (
    SELECT 
        CASE 
            WHEN DATEDIFF(YEAR, Birthdate, GETDATE()) BETWEEN 22 AND 35 THEN 'Young_Adult'
            WHEN DATEDIFF(YEAR, Birthdate, GETDATE()) BETWEEN 36 AND 49 THEN 'Adult'
            WHEN DATEDIFF(YEAR, Birthdate, GETDATE()) >= 50 THEN 'Old'
        END AS Age_group
    FROM Att
    WHERE Term_date IS NOT NULL
) AS Sub
GROUP BY Age_group
ORDER BY How_many DESC
```
![agee](https://github.com/user-attachments/assets/15f75e26-6b8c-40e1-beca-349b739ccf09)
#### Results show that there is no clear-cut distinction in attrition rates across age groups. This indicates that employee turnover is relatively evenly distributed, suggesting that factors driving attrition may not be age-specific but rather linked to broader organizational issues such as company culture, job roles, management practices, or work-life balance. It highlights the need for a more nuanced approach to retention strategies that consider diverse employee experiences beyond just age demographics

### Conclusion 
This exploratory analysis of employee attrition revealed several important trends. The highest attrition rates were observed in the headquarters, suggesting that in-office employees may be facing workplace-related challenges such as stricter oversight, less flexibility, or job dissatisfaction compared to their remote counterparts.

In terms of departmental turnover, specific departments showed noticeably higher attrition, indicating possible issues with departmental management, workload, or career progression opportunities that warrant further investigation.

Interestingly, age-based attrition was relatively balanced across all groups, suggesting that employee exits are influenced more by organizational factors than by age demographics. This finding implies that retention strategies should focus on improving the overall employee experience rather than targeting specific age segments.

Overall, this analysis provides a foundational understanding of attrition patterns and highlights key areas where HR efforts can be focused to reduce turnover and improve employee satisfaction.


 
