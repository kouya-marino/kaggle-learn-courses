# Group By, Having & Count

*Intro to SQL — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/group-by-having-count) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-group-by-having-count)

## Key ideas

- `COUNT()` with `GROUP BY` aggregates per group; `HAVING` filters groups.
- Aliases with `AS` make the output columns readable.

## Functions and tools used

`bigquery.Client`, `client.dataset`, `client.get_dataset`, `.table`, `client.get_table`, `.to_dataframe`, `client.list_rows`, `bigquery.QueryJobConfig`, `client.query`, `.head`

## Exercise

### `q_1` — 1) Prolific commenters

**My answer:**

```python
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
prolific_commenters_query = """
                            SELECT `by` AS author, COUNT(1) AS NumPosts
                            FROM `bigquery-public-data.hacker_news.full`
                            GROUP BY author
                            HAVING COUNT(1) > 10000
                            """
prolific_commenters = client.query(prolific_commenters_query, job_config=safe_config).to_dataframe()
print(prolific_commenters.head())
```

### `q_2` — 2) Deleted comments

**My answer:**

```python
deleted_posts = client.query("""
                    SELECT COUNT(1) AS num_deleted_posts
                    FROM `bigquery-public-data.hacker_news.full`
                    WHERE deleted = True
                    """, job_config=safe_config).to_dataframe()
num_deleted_posts = int(deleted_posts.num_deleted_posts.iloc[0])
print(num_deleted_posts)
```
