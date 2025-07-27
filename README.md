# 🗃️ SQL Query Execution Analysis on Normalized Database

## 📌 Project Overview

This project explores the performance of complex SQL queries on an SQLite database using **normalized schema design** and **datasets of increasing sizes (1MB, 10MB, 100MB)**. Query execution times are measured and compared across datasets to evaluate how performance scales with volume and query complexity.

## 🧠 Objective

- Design a relational schema in **3NF** with appropriate foreign key constraints  
- Execute complex SQL queries involving **joins**, **filters**, **aggregations**, and **subqueries**  
- Measure **execution time** across varying dataset sizes  
- Analyze scalability limitations of **SQLite** as database size increases


## 🧪 Dataset Details

- Three CSV files:  
  - `salary_tracker_1MB.csv`  
  - `salary_tracker_10MB.csv`  
  - `salary_tracker_100MB.csv`

- Fields include:  
  `PersonName`, `SchoolName`, `DepartmentName`, `BirthDate`, `JobTitle`, `Earnings`, `EarningsYear`, etc.

## 🧱 Database Schema Design

Normalized to **Third Normal Form (3NF)** with the following tables:

- `Person`: `PersonID`, `PersonName`, `BirthDate`, `StillWorking`
- `School`: `SchoolID`, `SchoolName`, `SchoolCampus`
- `Department`: `DepartmentID`, `DepartmentName`
- `Job`: `JobID`, `JobTitle`, `DepartmentID` (FK)
- `Salary`: `PersonID`, `JobID`, `SchoolID`, `Earnings`, `EarningsYear`  
  - Composite Primary Key: (`PersonID`, `JobID`, `EarningsYear`)  
  - Foreign Keys: references to `Person`, `School`, `Job`

## 🧾 Queries Executed

1. **High Earners Born Before 1975**  
2. **Non-working individuals earning over $400K**  
3. **Former Lecturers at University of Texas**  
4. **Campus with most active faculty**  
5. **Most recent salary of Madison Harrison**  
6. **Department with highest average earnings**

## ⏱️ Execution Time Results

| Dataset Size | q1     | q2     | q3     | q4     | q5     | q6     |
|--------------|--------|--------|--------|--------|--------|--------|
| **1MB**      | 3.63ms | 0.92ms | 1.31ms | 1.81ms | 1.18ms | 2.96ms |
| **10MB**     | 33.4ms | 8.36ms | 13.1ms | 16.1ms | 10.6ms | 29.9ms |
| **100MB**    | 317.8ms| 84.7ms | 150.8ms| 187.8ms| 108.0ms| 331.0ms|

✅ Execution time **increased significantly** with dataset size  
✅ Most expensive queries: `q1`, `q6` (due to subqueries and aggregations)

## 📊 Observations

- SQLite performs well on small datasets but **slows down significantly** with size and complexity  
- Normalized schema improves **data consistency and structure**, but query planning becomes critical  
- Subqueries and joins have **higher performance cost** with larger data

## 🛠 Tools Used

- SQLite  
- Python 3.x  
- `sqlite3`, `pandas`, `time`  
- Jupyter Notebook
