# 🎬 Netflix Movies and TV Shows Data Analysis using SQL

![](https://github.com/bprasad03/netflix-data-analysis-sql/blob/main/logo.jpg)

## 📘 Overview

This project performs an in-depth analysis of Netflix’s Movies and TV Shows dataset using **SQL**.  
It explores Netflix’s global catalog to uncover trends across **genres, release years, ratings, and regions**, with a special focus on **Indian content growth**.  

The goal is to demonstrate SQL proficiency through practical, data-driven insights using aggregate functions, string operations, window functions, and date manipulation.

---

## 🎯 Objectives

- Compare the number of **Movies vs. TV Shows** on Netflix.  
- Identify the **most common ratings** for each content type.  
- Analyze **release year trends** and **top content-producing countries**.  
- Explore **genre diversity**, **actor participation**, and **regional insights**.  
- Detect **keyword-based content categorization** (e.g., “kill” or “violence”).  

---

## 📂 Dataset

- **Source:** [Netflix Movies and TV Shows Dataset – Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)
- **Description:** This dataset contains detailed metadata about Netflix titles including:
  - `title`, `director`, `cast`, `country`, `release_year`, `rating`, `duration`, `listed_in`, and `description`.

---

## 🧱 Database Schema

```sql
CREATE TABLE netflix
(
	show_id	      VARCHAR(5),
	type          VARCHAR(10),
	title	      VARCHAR(250),
	director      VARCHAR(550),
	casts	      VARCHAR(1050),
	country	      VARCHAR(550),
	date_added	  VARCHAR(55),
	release_year  INT,
	rating	      VARCHAR(15),
	duration	  VARCHAR(15),
	listed_in	  VARCHAR(250),
	description   VARCHAR(550)
);
```

## Business Problems and Solutions

### 1. Count the Number of Movies vs TV Shows

```sql
SELECT 
    type,
    COUNT(*)
FROM netflix
GROUP BY 1;
```

### 2️⃣ Find the Most Common Rating for Movies and TV Shows
```sql
SELECT 
    type,
    rating,
    COUNT(*) AS total
FROM netflix
GROUP BY type, rating
HAVING COUNT(*) = (
    SELECT MAX(counts) 
    FROM (
        SELECT COUNT(*) AS counts
        FROM netflix n2
        WHERE n2.type = netflix.type
        GROUP BY rating
    ) AS subquery
);

### 3️⃣ List All Movies Released in a Specific Year (e.g., 2020)

```sql
SELECT * 
FROM netflix
WHERE type = 'Movie' 
  AND release_year = 2020;




