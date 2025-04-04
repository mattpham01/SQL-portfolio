/* 
Dataset: Banking Dataset Marketing Targets
Source: https://www.kaggle.com/datasets/prakharrathi25/banking-dataset-marketing-targets/data
Query Editor: pgAdmin 4
/*

--Create table and import that dataset from Kaggle
CREATE TABLE train(
  age INTEGER,
  job VARCHAR(20),
  marital VARCHAR(20),
  education VARCHAR(20),
  has_default BOOLEAN, 
  balance INTEGER,
  housing BOOLEAN,
  loan BOOLEAN,
  contact TEXT, 
  day INTEGER,
  month TEXT,
  duration INTEGER,
  campaign INTEGER,
  pday INTEGER,
  previous INTEGER,
  poutcome TEXT,
  y BOOLEAN
);

--Busines Questions 
--1. How many customers are in the data set?

SELECT COUNT(*) AS total_customers
FROM train


--2. What is the average age of our customers?

SELECT ROUND(AVG(age)) AS avg_age
FROM train



--3. What is the distribution of job types?

SELECT job, COUNT(*) AS job_count, AVG(balance) AS average_banalce
FROM train 
GROUP BY job
ORDER BY AVG(balance) DESC;

--4. How many customers are married, single, or divorced?

SELECT marital, COUNT(*) AS count
FROM train 
GROUP BY marital
ORDER BY COUNT DESC;


--5. What is the average balance of customers?

SELECT age, AVG(balance) AS avg_balance 
FROM train 
GROUP BY age
ORDER BY age DESC;

--6. How many customers have housing loans? Personal loans?

SELECT housing, COUNT(*) AS count
FROM train 
GROUP BY housing

SELECT loan, COUNT(*) AS count 
FROM train
GROUP BY loan

--7. What is the average duration of the last contact?

SELECT AVG(duration) AS avg_duration 
FROM train

--8. What age group is most likely to subscribe to a term deposit? 

SELECT age, COUNT(y) AS sub_term_deposit
FROM train 
WHERE y = 'True'
GROUP BY age
ORDER BY COUNT(y) DESC;





























