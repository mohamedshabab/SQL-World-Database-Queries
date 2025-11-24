# 🌍 World SQL Analysis Project (MySQL)

This project explores the MySQL **`world`** database using SQL queries focused on real demographic and geographic analysis.  
Using tasks taken from the Week 3 workbook (only the sections related to the *world* dataset), I practiced retrieving, filtering, sorting, joining, and aggregating global data across countries, cities, and languages.

The goal of this project is to demonstrate practical SQL skills used in data analytics while analyzing real-world datasets such as population distribution, language usage, and country-level metrics.

----

## 📁 Database Overview

This project uses the classic MySQL **`world`** database — a structured dataset containing real-world information about countries, cities, and languages around the globe.  
The tasks completed for this project come from the Week 3 workbook, specifically the sections designed for practicing SQL queries on the *world* dataset.

### 🌍 Key Tables in the `world` Database

- 🌐 **`Country`** — country name, continent, region, population, life expectancy, GNP  
- 🏙️ **`City`** — city name, country code, district, and population  
- 🗣️ **`CountryLanguage`** — languages spoken in each country and whether they are official  

These tables form a fully relational structure used for exploring demographics, population metrics, and language distribution.

### 📄 Files Used

- **create world db .sql** — SQL script used to create and load the `world` database  
- **Data_Technician_Workbook_Week_3 Workbench use.docx** — used only for the *world database tasks* (Day 2 / Day 3 tasks related to Country, City, CountryLanguage)

Only the relevant workbook tasks involving the `world` database were included in this project.

---

## 🎯 Project Objectives

The goal of this SQL project is to practice real data-analysis techniques using the MySQL **`world`** database.  
The exercises focus on exploring global demographics, population insights, and language distributions through practical SQL querying.

### **Key Objectives**
- Understand the structure of the `world` database (Country, City, CountryLanguage)
- Use `SELECT` and `FROM` to retrieve global data
- Filter records with `WHERE`
- Sort results using `ORDER BY`
- Use `LIMIT` to control output size
- Query continental and regional statistics
- Analyze population distributions across cities and countries
- Explore official vs. non-official languages
- Write clean and readable SQL queries modeled on real-world analytic tasks

These objectives reflect practical SQL skills used in data research, reporting, and geographical analysis.

---

## 🛠️ SQL Skills Practiced

Throughout this project, I used the MySQL **`world`** database to strengthen fundamental SQL query-writing skills.  
These exercises focus on retrieving, filtering, and analyzing real global demographic data.

### 📌 Core SQL Concepts
- `SELECT` — retrieve specific columns  
- `FROM` — choose the source table  
- `WHERE` — filter rows based on conditions  
- `ORDER BY` — sort results  
- `LIMIT` — restrict output  

### 🔗 Understanding Relationships
Worked across the three main tables:
- `Country`  
- `City`  
- `CountryLanguage`

Practiced how these tables relate through primary and foreign keys:
- `Country.Code` → `City.CountryCode`  
- `Country.Code` → `CountryLanguage.CountryCode`

### 🔢 Grouping & Aggregation
Used:
- `GROUP BY`  
- `COUNT()`  
- `SUM()`  
- `AVG()`  
- `MAX()` / `MIN()`

To answer questions such as:
- total number of cities in a country  
- largest populations by region  
- language distribution percentages  

### 🌍 Data Exploration Skills
- Identify top-populated countries and cities  
- Compare population density across continents  
- Explore official vs. non-official languages  
- Analyze regional population totals  

These skills reflect real data-analysis workflows when working with geographic or demographic databases.

---

## 🔍 Analysis Highlights

Below are the key SQL exercises completed using the **MySQL World Database**.  
Each query highlights a specific concept such as filtering, joining tables, grouping, and aggregating global data.

---

### 🧾 1. List All Countries (Basic SELECT)
Retrieves country name, continent, and population from the `country` table.

```sql
SELECT Name,
       Continent,
       Population
FROM country;

```
### 🏙️ 2. Cities in a Specific Country

Example: All cities in Canada.

```sql
SELECT city.Name,
       city.Population
FROM city
JOIN country
      ON city.CountryCode = country.Code
WHERE country.Name = 'Canada';


```
### 🌍 3. Total Population by Continent

Uses GROUP BY to aggregate population.

```sql
SELECT Continent,
       SUM(Population) AS TotalPopulation
FROM country
GROUP BY Continent
ORDER BY TotalPopulation DESC;


```
### 🗣️ 4. Most Spoken Languages (by number of speakers)

Uses a join between countrylanguage and country.

```sql
SELECT cl.Language,
       SUM(c.Population * cl.Percentage / 100) AS TotalSpeakers
FROM countrylanguage cl
JOIN country c
      ON cl.CountryCode = c.Code
GROUP BY cl.Language
ORDER BY TotalSpeakers DESC;


```
### 🏆 5. Top 10 Most Populated Cities in the World

Demonstrates sorting and limiting results.

```sql
SELECT Name,
       CountryCode,
       Population
FROM city
ORDER BY Population DESC
LIMIT 10;

```
### 📊 6. Average Life Expectancy by Continent

Shows use of AVG() with grouping.

```sql
SELECT Continent,
       AVG(LifeExpectancy) AS AvgLifeExpectancy
FROM country
WHERE LifeExpectancy IS NOT NULL
GROUP BY Continent
ORDER BY AvgLifeExpectancy DESC;


```
### 🧮 7. Number of Cities per Country

Counts related rows using a join.

```sql
SELECT country.Name AS Country,
       COUNT(city.ID) AS NumberOfCities
FROM country
LEFT JOIN city
       ON country.Code = city.CountryCode
GROUP BY country.Name
ORDER BY NumberOfCities DESC;


```
### 📌 8. Countries With Multiple Official Languages

Filters using a HAVING clause.

```sql
SELECT country.Name,
       COUNT(countrylanguage.Language) AS NumOfficialLanguages
FROM country
JOIN countrylanguage
      ON country.Code = countrylanguage.CountryCode
WHERE countrylanguage.IsOfficial = 'T'
GROUP BY country.Name
HAVING NumOfficialLanguages > 1
ORDER BY NumOfficialLanguages DESC;

```
-----
## 🎓 Learning Outcomes

Working with the MySQL **World Database** helped strengthen a wide range of SQL and data analysis skills.  
Through the exercises, I gained hands-on experience with real relational data, global demographic insights, and multi-table querying.

### 🔹 SQL Query Writing
- Retrieved specific columns using `SELECT`
- Filtered rows using `WHERE`
- Sorted results using `ORDER BY`
- Limited output with `LIMIT`
- Wrote clean, readable, and structured SQL queries

### 🔹 Joining Tables
- Connected related tables using `INNER JOIN` and `LEFT JOIN`
- Joined:
  - `country` ↔ `city`
  - `country` ↔ `countrylanguage`
- Combined fields across datasets to answer real analytical questions

### 🔹 Grouping & Aggregation
Used aggregate functions to summarize global data:
- `SUM()` — total population per continent  
- `COUNT()` — number of cities per country  
- `AVG()` — life expectancy averages  
- `MAX()` / `MIN()` for additional insight  
- `HAVING` for grouped filtering (e.g., countries with multiple official languages)

### 🔹 Real-World Data Interpretation
Analyzed:
- Population distribution by continent  
- Top populated cities  
- Most spoken languages worldwide  
- Country-level city counts  
- Life expectancy trends  
- Countries with multilingual official status  

### 🔹 Database & Schema Understanding
- Explored relationships between tables using foreign keys  
- Understood the structure of a normalized database  
- Learned how global datasets can be modeled relationally

These exercises improved my ability to work confidently with SQL databases and extract meaningful insights from structured data.  
They also helped strengthen query-building logic and analytical thinking—skills used daily in real data analysis work.


----

## 📌 Conclusion

This World Database SQL project provided a practical, hands-on way to explore and analyze global demographic data using real SQL techniques.  
Through structured tasks, I queried countries, cities, populations, and languages—building insights that reflect real-world analytical workflows.

By using `SELECT`, filtering with `WHERE`, joining tables, and applying grouped aggregations, I was able to answer meaningful questions such as:

- Which countries have the largest populations?
- Which cities are the most populated?
- How many languages are spoken in each country?
- Which continents hold most of the world’s population?
- Which countries have the highest life expectancy?

The project strengthened my ability to work with relational datasets, interpret structured global information, and write efficient SQL queries for analysis.  
Overall, it demonstrates strong capability in SQL querying, database understanding, and extracting business-ready insights from real-world data.

---

## 🖥️ How to Use This Project

This repository includes all SQL files and tasks required to recreate and run the World Database exercises:

### 📄 Files Included
- **create_world_db.sql** — creates and loads the full World database  
- **world_queries.sql** — contains the queries used in this project (optional if you add it)  
- Selected tasks from the workbook (City, Country, CountryLanguage queries)

### ▶️ How to Run the Project

1. **Open your SQL environment:**  
   MySQL Workbench / pgAdmin / Azure Data Studio / MariaDB / any SQL client of your choice.

2. **Load the World database:**
   ```sql
   SOURCE create_world_db.sql;
