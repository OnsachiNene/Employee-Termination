# Welcome to my Employee Termination Exploratory Analysis! Stay with me as we uncover the secrets of this dataset

### This Project is all about:
- Cleaning and Norminalizing jumbled datasets
- Perfoming CRUD operations to answer burning questions
- Putting all of this information in a picture, i mean, its worth more than a thousand words anyway.
  
### Data Source
#### On a very sunny day while i was lazying away, my friend, Ben (Pseudo name) sent me this dataset, ill ask her where exactly she got it from. The data set is saved as "Try this. csv". It contains information about the employees, you know, regular stuff, Id, department and so on, as well as their hire and termination dates.

### Tools used
- Excel (Data Cleaning)
- Sql (CRUD Operations)
- Power Bi (Visualization)

### Lets get into business, or should i say Queryness 
#### Data cleaning and Preparation: 
#### First the data was loaded using Excel for inspection and Power query to clean up the data (Changing data types, Replacing Values, Handling missing values)
#### Data was then imported into Sql where i used CRUD Operations to Select, Aggregate, Count and fiter results as the case may be. I also did some data cleaning here too as cleaning is a continuous process...really. 

### Exploratory Analysis. 
- For this data set i wanted to find out the following
  1. What department had the highest attrition rate?
  2. What Location (Head quarter or Remote) has the highest attrition rate
  3. What Age group has the highest Attrition rate
  4. Correlation between Employee Location and Attrition

### SQL in action 
#### At this stage, before i start doing any serious digging, i want to be sure, once again that my data has no duplicates. 
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
### What department has the highest staff termination 
```sql
SELECT Department, COUNT (Department) as Count 
  FROM Att 
  WHERE Term_date IS NOT NULL 
  GROUP BY Department 
  ORDER BY Count DESC
```
![Dep 2](https://github.com/user-attachments/assets/8af95fc2-345d-4f79-a990-21e2cd7bd198)

### What Location (Head quarter or Remote) has the highest attrition rate?
```sql
SELECT Location, COUNT (Location)How_many 
  FROM Att 
  WHERE Term_date IS NOT NULL 
  GROUP BY Location 
  ORDER BY How_many DESC
```
 ![location](https://github.com/user-attachments/assets/7ab2175b-2422-4e2a-9d46-d6fd09e21414)


### What Age group has the highest Attrition rate?
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




 
