# my-first-project_titanic_data
Through this project, we explore how SQL can help uncover trends and patterns in large datasets and support data-driven decision-making.
create database SQL_PROJECT;
use SQL_PROJECT;

SELECT * FROM sql_project.`titanic-dataset`;

-- 1ST QUESTION) How many passengers were in each class (Pclass)?


select Pclass, 
             count(Pclass) as Total_Passanger 
             from sql_project.`titanic-dataset` 
group by Pclass ; 
                         
-- 2ND QUESTION) How many passengers were on the Titanic?


select Count(*) 
         As Total_passanger_on_Titanic 
from sql_project.`titanic-dataset` ;



-- 3RD QUESTION) What is the average age of the passengers?


Select 
      AVG(age) AS TOTAL_AVERAGE_OF_AGE 
from sql_project.`titanic-dataset` ;



-- 4TH QUESTION) How many male and female passengers were there?

Select sex, 
       Count(sex) AS TOTAL_MALE_FEMAL 
       from sql_project.`titanic-dataset`
group by sex;


-- 5TH QUESTION) What was the survival rate by gender?

SELECT
  Sex,
  COUNT(*) AS Total,
  SUM(Survived) AS Survived_Count,
  ROUND(AVG(Survived) * 100, 2) AS Survival_Rate_Percentage
FROM
  sql_project.`titanic-dataset`
GROUP BY
  Sex;


-- 6TH QUESTION) Which cabin had the most survivors?

SELECT
  Cabin,
  COUNT(*) AS Survivors
FROM
  sql_project.`titanic-dataset`
WHERE
  Survived = 1 AND Cabin IS NOT NULL
GROUP BY
  Cabin
ORDER BY
  Survivors DESC
LIMIT 1;


-- 7TH QUESTION) Categorize passengers based on their class (Pclass) into "Economy", "Business", and "First Class" groups.

SELECT
  PassengerId,
  Name,
  Pclass,
  CASE 
    WHEN Pclass = 1 THEN 'First Class'
    WHEN Pclass = 2 THEN 'Business'
    WHEN Pclass = 3 THEN 'Economy'
    ELSE 'Unknown'
  END AS Class_Category
FROM
  sql_project.`titanic-dataset`;
  
  
-- 8TH QUESTION) What is the rank of passengers based on their fare within each class (Pclass)?


SELECT
  PassengerId,
  Name,
  Pclass,
  Fare,
  RANK() OVER (
    PARTITION BY Pclass
    ORDER BY Fare DESC
  ) AS Fare_Rank_Within_Class
FROM
sql_project.`titanic-dataset`;


-- 9TH QUESTION) What is the first (lowest) fare paid by passengers in each class (Pclass)?

SELECT
  Pclass,
  MIN(Fare) AS Lowest_Fare
FROM
  sql_project.`titanic-dataset`
GROUP BY
  Pclass;


