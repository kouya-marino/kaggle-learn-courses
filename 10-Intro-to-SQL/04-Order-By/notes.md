# Order By

*Intro to SQL — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/order-by) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-order-by)

## Key ideas

- `ORDER BY ... DESC` sorts results; `EXTRACT(... FROM timestamp)` pulls parts of dates.
- Combine with `GROUP BY` / `HAVING` for ranked summaries.

## Functions and tools used

`bigquery.Client`, `client.dataset`, `client.get_dataset`, `.table`, `client.get_table`, `.to_dataframe`, `client.list_rows`, `bigquery.QueryJobConfig`, `client.query`

## Exercise

### `q_1` — Query to find out the number of accidents for each day of the week

**My answer:**

```python
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
country_spend_pct_query = """
                          SELECT country_name, AVG(value) AS avg_ed_spending_pct
                          FROM `bigquery-public-data.world_bank_intl_education.international_education`
                          WHERE indicator_code = 'SE.XPD.TOTL.GD.ZS' and year >= 2010 and year <= 2017
                          GROUP BY country_name
                          ORDER BY avg_ed_spending_pct DESC
                          """
country_spending_results = client.query(country_spend_pct_query, job_config=safe_config).to_dataframe()
print(country_spending_results.head())
```

### `q_2` — 2) Identify interesting codes to explore

**My answer:**

```python
code_count_query = """
                   SELECT indicator_code, indicator_name, COUNT(1) AS num_rows
                   FROM `bigquery-public-data.world_bank_intl_education.international_education`
                   WHERE year = 2016
                   GROUP BY indicator_name, indicator_code
                   HAVING COUNT(1) >= 175
                   ORDER BY COUNT(1) DESC
                   """
code_count_results = client.query(code_count_query, job_config=safe_config).to_dataframe()
print(code_count_results.head())
```
