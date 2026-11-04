# Exercise (solved): As & With


**This notebook is an exercise in the [SQL](https://www.kaggle.com/learn/intro-to-sql) course.  You can reference the tutorial at [this link](https://www.kaggle.com/dansbecker/as-with).**

---

# Introduction

You are getting to the point where you can own an analysis from beginning to end. So you'll do more data exploration in this exercise than you've done before.  Before you get started, run the following set-up code as usual.

```python
# Get most recent checking code
!pip install -U -t /kaggle/working/ git+https://github.com/Kaggle/learntools.git
# Set up feedback system
from learntools.core import binder
binder.bind(globals())
from learntools.sql.ex5 import *
print("Setup Complete")
```

You'll work with a dataset about taxi trips in the city of Chicago. Run the cell below to fetch the `chicago_taxi_trips` dataset.

```python
from google.cloud import bigquery

# Create a "Client" object
client = bigquery.Client()

# Construct a reference to the "chicago_taxi_trips" dataset
dataset_ref = client.dataset("chicago_taxi_trips", project="bigquery-public-data")

# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)
```

# Exercises

You are curious how much slower traffic moves when traffic volume is high. This involves a few steps.

### 1) Find the data
Before you can access the data, you need to find the table name with the data.

*Hint*: Tab completion is helpful whenever you can't remember a command. Type `client.` and then hit the tab key. Don't forget the period before hitting tab.

```python
# Your code here to find the table name
```

```python
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
for t in client.list_tables(dataset):
    print(t.table_id)
table_name = 'taxi_trips'
q_1.check()
```

For the solution, uncomment the line below.

```python
#q_1.solution()
```

### 2) Peek at the data

Use the next code cell to peek at the top few rows of the data. Inspect the data and see if any issues with data quality are immediately obvious.

```python
# Your code here
```

After deciding whether you see any important issues, run the code cell below.

```python
# Check your answer (Run this code cell to receive credit!)
q_2.solution()
```

### 3) Determine when this data is from

If the data is sufficiently old, we might be careful before assuming the data is still relevant to traffic patterns today. Write a query that counts the number of trips in each year.  

Your results should have two columns:
- `year` - the year of the trips
- `num_trips` - the number of trips in that year

Hints:
- When using **GROUP BY** and **ORDER BY**, you should refer to the columns by the alias `year` that you set at the top of the **SELECT** query.
- The SQL code to **SELECT** the year from `trip_start_timestamp` is <code>SELECT EXTRACT(YEAR FROM trip_start_timestamp)</code>
- The **FROM** field can be a little tricky until you are used to it.  The format is:
    1. A backick (the symbol \`).
    2. The project name. In this case it is `bigquery-public-data`.
    3. A period.
    4. The dataset name. In this case, it is `chicago_taxi_trips`.
    5. A period.
    6. The table name. You used this as your answer in **1) Find the data**.
    7. A backtick (the symbol \`).

```python
rides_per_year_query = """
                       SELECT EXTRACT(YEAR FROM trip_start_timestamp) AS year,
                              COUNT(1) AS num_trips
                       FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
                       GROUP BY year
                       ORDER BY year
                       """
rides_per_year_query_job = client.query(rides_per_year_query, job_config=safe_config)
rides_per_year_result = rides_per_year_query_job.to_dataframe()
print(rides_per_year_result)
q_3.check()
```

For a hint or the solution, uncomment the appropriate line below.

```python
#q_3.hint()
#q_3.solution()
```

### 4) Dive slightly deeper

You'd like to take a closer look at rides from 2016.  Copy the query you used above in `rides_per_year_query` into the cell below for `rides_per_month_query`.  Then modify it in two ways:
1. Use a **WHERE** clause to limit the query to data from 2016.
2. Modify the query to extract the month rather than the year.

```python
rides_per_month_query = """
                        SELECT EXTRACT(MONTH FROM trip_start_timestamp) AS month,
                               COUNT(1) AS num_trips
                        FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
                        WHERE EXTRACT(YEAR FROM trip_start_timestamp) = 2016
                        GROUP BY month
                        ORDER BY month
                        """
rides_per_month_query_job = client.query(rides_per_month_query, job_config=safe_config)
rides_per_month_result = rides_per_month_query_job.to_dataframe()
print(rides_per_month_result)
q_4.check()
```

For a hint or the solution, uncomment the appropriate line below.

```python
#q_4.hint()
#q_4.solution()
```

### 5) Write the query

It's time to step up the sophistication of your queries.  Write a query that shows, for each hour of the day in the dataset, the corresponding number of trips and average speed.

Your results should have three columns:
- `hour_of_day` - sort by this column, which holds the result of extracting the hour from `trip_start_timestamp`.
- `num_trips` - the count of the total number of trips in each hour of the day (e.g. how many trips were started between 6AM and 7AM, independent of which day it occurred on).
- `avg_mph` - the average speed, measured in miles per hour, for trips that started in that hour of the day.  Average speed in miles per hour is calculated as `3600 * SUM(trip_miles) / SUM(trip_seconds)`. (The value 3600 is used to convert from seconds to hours.)

Restrict your query to data meeting the following criteria:
- a `trip_start_timestamp` > **2016-01-01** and < **2016-04-01**
- `trip_seconds` > 0 and `trip_miles` > 0

You will use a common table expression (CTE) to select just the relevant rides.  Because this dataset is very big, this CTE should select only the columns you'll need to create the final output (though you won't actually create those in the CTE -- instead you'll create those in the later **SELECT** statement below the CTE).

This is a much harder query than anything you've written so far.  Good luck!

```python
speeds_query = """
               WITH RelevantRides AS
               (
                   SELECT EXTRACT(HOUR FROM trip_start_timestamp) AS hour_of_day,
                          trip_miles,
                          trip_seconds
                   FROM `bigquery-public-data.chicago_taxi_trips.taxi_trips`
                   WHERE trip_start_timestamp > '2016-01-01' AND
                         trip_start_timestamp < '2016-04-01' AND
                         trip_seconds > 0 AND
                         trip_miles > 0
               )
               SELECT hour_of_day,
                      COUNT(1) AS num_trips,
                      3600 * SUM(trip_miles) / SUM(trip_seconds) AS avg_mph
               FROM RelevantRides
               GROUP BY hour_of_day
               ORDER BY hour_of_day
               """
speeds_query_job = client.query(speeds_query, job_config=safe_config)
speeds_result = speeds_query_job.to_dataframe()
print(speeds_result)
q_5.check()
```

For the solution, uncomment the appropriate line below.

```python
#q_5.solution()
```

That's a hard query. If you made good progress towards the solution, congratulations!

# Keep going

You can write very complex queries now with a single data source. But nothing expands the horizons of SQL as much as the ability to combine or **JOIN** tables.

**[Click here](https://www.kaggle.com/dansbecker/joining-data)** to start the last lesson in the Intro to SQL course.

---




*Have questions or comments? Visit the [course discussion forum](https://www.kaggle.com/learn/intro-to-sql/discussion) to chat with other learners.*
