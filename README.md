Home Sales Data Analysis Using SparkSQL

Project Overview

The Module 22 Challenge focuses on analyzing home sales data using PySpark and SparkSQL. The project involves creating temporary views, partitioning data, caching tables, and performing complex queries to extract insights such as average home prices based on specific criteria. By leveraging Spark’s distributed computing capabilities, the project also compares runtimes for cached and uncached operations to highlight performance optimizations.

This project was completed using Google Colab to ensure seamless integration with PySpark and access to a distributed computing environment.

Technologies Used
	•	Programming Language: Python
	•	Libraries: PySpark, SparkSQL
	•	Data Formats: CSV, Parquet
	•	Tools: Google Colab, Git/GitHub

Project Steps
1. Data Import and SparkSession Setup
	•	The home_sales_revised.csv dataset is read into a Spark DataFrame.
	•	A SparkSession is initialized to enable SparkSQL operations.
	•	The dataset is transformed into a temporary table named home_sales.

2. Creating Temporary Tables
	•	A temporary table, home_sales, is created to allow SQL-like querying on the home sales dataset.
	•	The dataset is explored using SparkSQL queries.

3. SQL Queries
Key queries executed:
	1.	Average Price for Four-Bedroom Homes by Year

        SELECT YEAR(date) AS year, ROUND(AVG(price), 2) AS avg_price
        FROM home_sales
        WHERE bedrooms = 4
        GROUP BY YEAR(date)
        ORDER BY year;

    2.	Average Price of 3-Bedroom, 3-Bathroom Homes by Year Built

        SELECT date_built, ROUND(AVG(price), 2) AS avg_price
        FROM home_sales
        WHERE bedrooms = 3 AND bathrooms = 3
        GROUP BY date_built
        ORDER BY date_built;
    
    3.	Average Price of 3-Bedroom, 3-Bathroom, Two-Floor Homes (≥2000 sqft)

        SELECT date_built, ROUND(AVG(price), 2) AS avg_price
        FROM home_sales
        WHERE bedrooms = 3 AND bathrooms = 3 AND floors = 2 AND sqft_living >= 2000
        GROUP BY date_built
        ORDER BY date_built;

	4.	Average Price per View Rating for Homes (≥$350,000)

        SELECT view AS view_rating, ROUND(AVG(price), 2) AS avg_price
        FROM home_sales
        GROUP BY view
        HAVING AVG(price) >= 350000
        ORDER BY view_rating DESC;

4. Caching and Performance
	•	The home_sales temporary table is cached to optimize repeated query execution.
	•	Query runtimes are measured for cached and uncached operations to demonstrate performance improvements.

5. Partitioning and Parquet Format
	•	The dataset is partitioned by the date_built field and stored in Parquet format for efficient data storage and retrieval.
	•	A temporary table for the partitioned Parquet data is created, and the last query is executed to compare runtimes.

Conclusion

This project demonstrates the power of PySpark in analyzing large datasets efficiently. It highlights:
	•	Using SparkSQL for querying and transforming data.
	•	Optimizing performance with caching.
	•	Partitioning and converting data to Parquet format for better storage and access.

This entire project was executed in Google Colab, which provided an ideal environment for PySpark integration and distributed computing capabilities.

Credits

This project was developed by Elizabeth Conn as part of the Module 22 Challenge.