# As & With

*Intro to SQL — lesson 5* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/as-with) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-as-with)

## Key ideas

- `AS` renames columns; `WITH ... AS (...)` defines common table expressions.
- CTEs break long queries into readable steps.

## Functions and tools used

`bigquery.Client`, `client.dataset`, `client.get_dataset`, `.table`, `client.get_table`, `.to_dataframe`, `client.list_rows`, `bigquery.QueryJobConfig`, `client.query`, `.head`, `.plot`, `.set_index`

## Exercise

### `q_1` — 1) Find the data

**My answer:**

```python
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
for t in client.list_tables(dataset):
    print(t.table_id)
table_name = 'taxi_trips'
```

### `q_2` — 2) Peek at the data

**Discussion:** You can see the data by calling: 
```python
# Construct a reference to the "taxi_trips" table
table_ref = dataset_ref.table("taxi_trips")

# API request - fetch the table
table = client.get_table(table_ref)

# Preview the first five lines of the "taxi_trips" table
client.list_rows(table, max_results=5).to_dataframe()
```

Some location fields have values of `None` or `NaN`. That is a problem if we want to use those fields.

### `q_3` — 3) Determine when this data is from

**My answer:**

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
```

### `q_4` — 4) Dive slightly deeper

**My answer:**

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
```

### `q_5` — 5) Write the query

**My answer:**

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
```

### `q_6`

**Discussion:** The results show rides with hours 1-12. But there should be results in the afternoon (hours 13-24).

Perhaps the raw data has lost the distinction between AM and PM values.

You can review 200 rows of the raw data with the commands: 
```python
# Construct a reference to the "taxi_trips" table
table_ref = dataset_ref.table("taxi_trips")

# API request - fetch the table
table = client.get_table(table_ref)

# Preview the first five lines of the "taxi_trips" table
client.list_rows(table, max_results=200).to_dataframe()
```

You'll see that the timestamps are all in the AM hours (hours are less than or equal to 12.) 

At first you might worry that the data is coming back sorted by time, but the variety of dates suggests that's not the case. 
Part of data science is tracking down exactly this type of problem. If you were in an organization working on this, you could show the evidence you've just collected (e.g. the breakdown of trips by hour) to someone responsible for collecting the data, and help them debug the data collection and storage process.
