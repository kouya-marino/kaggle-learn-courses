# Getting Started With SQL and BigQuery

*Intro to SQL — lesson 1* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/getting-started-with-sql-and-bigquery) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-getting-started-with-sql-and-bigquery)

## Key ideas

- BigQuery workflow: `Client` → dataset reference → table reference → schema.
- `list_rows(...).to_dataframe()` previews a table.

## Functions and tools used

`bigquery.Client`, `client.dataset`, `client.get_dataset`, `client.list_tables`, `.table`, `client.get_table`, `.to_dataframe`, `client.list_rows`

## Exercise

### `q_1` — 1) Count tables in the dataset

**My answer:**

```python
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
tables = list(client.list_tables(dataset))
num_tables = len(tables)
```

### `q_2` — 2) Explore the table schema

**My answer:**

```python
table = client.get_table(dataset_ref.table("crime"))
num_timestamp_fields = sum(1 for f in table.schema if f.field_type == "TIMESTAMP")
print(num_tables, num_timestamp_fields)
```

### `q_3` — 3) Create a crime map

**My answer:**

```python
fields_for_plotting = ['latitude', 'longitude']
```
