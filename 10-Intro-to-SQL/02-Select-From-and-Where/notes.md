# Select, From & Where

*Intro to SQL — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/select-from-where) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-select-from-where)

## Key ideas

- `SELECT columns FROM table WHERE condition`.
- Limit cost with `QueryJobConfig(maximum_bytes_billed=...)`; `to_dataframe()` returns results.

## Functions and tools used

`bigquery.Client`, `client.dataset`, `client.get_dataset`, `client.list_tables`, `.table`, `client.get_table`, `.to_dataframe`, `client.list_rows`, `client.query`, `.head`, `.value_counts`, `bigquery.QueryJobConfig`

## Exercise

### `q_1` — 1) Units of measurement

**My answer:**

```python
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
first_query = """
              SELECT country
              FROM `bigquery-public-data.openaq.global_air_quality`
              WHERE unit = "ppm"
              """
first_results = client.query(first_query, job_config=safe_config).to_dataframe()
print(first_results.head())
```

### `q_2` — 2) High air quality

**My answer:**

```python
zero_pollution_query = """
                       SELECT *
                       FROM `bigquery-public-data.openaq.global_air_quality`
                       WHERE value = 0
                       """
zero_pollution_results = client.query(zero_pollution_query, job_config=safe_config).to_dataframe()
print(zero_pollution_results.head())
```
