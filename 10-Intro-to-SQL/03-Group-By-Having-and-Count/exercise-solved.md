# Exercise (solved): Group By, Having & Count


**This notebook is an exercise in the [SQL](https://www.kaggle.com/learn/intro-to-sql) course.  You can reference the tutorial at [this link](https://www.kaggle.com/dansbecker/group-by-having-count).**

---

# Introduction

Queries with **GROUP BY** can be powerful. There are many small things that can trip you up (like the order of the clauses), but it will start to feel natural once you've done it a few times. Here, you'll write queries using **GROUP BY** to answer questions from the Hacker News dataset.

Before you get started, run the following cell to set everything up:

```python
# Set up feedback system
from learntools.core import binder
binder.bind(globals())
from learntools.sql.ex3 import *
print("Setup Complete")
```

The code cell below fetches the `full` table from the `hacker_news` dataset.  We also preview the first five rows of the table.

```python
from google.cloud import bigquery

# Create a "Client" object
client = bigquery.Client()

# Construct a reference to the "hacker_news" dataset
dataset_ref = client.dataset("hacker_news", project="bigquery-public-data")

# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)

# Construct a reference to the "full" table
table_ref = dataset_ref.table("full")

# API request - fetch the table
table = client.get_table(table_ref)

# Preview the first five lines of the table
client.list_rows(table, max_results=5).to_dataframe()
```

# Exercises

### 1) Prolific commenters

Hacker News would like to send awards to everyone who has written more than 10,000 posts. Write a query that returns all authors with more than 10,000 posts as well as their post counts. Call the column with post counts `NumPosts`.

In case sample query is helpful, here is a query you saw in the tutorial to answer a similar question:
```
query = """
        SELECT parent, COUNT(1) AS NumPosts
        FROM `bigquery-public-data.hacker_news.full`
        GROUP BY parent
        HAVING COUNT(1) > 10
        """
```

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
q_1.check()
```

For the solution, uncomment the line below.

```python
#q_1.solution()
```

### 2) Deleted comments

How many comments have been deleted? (If a comment was deleted, the `deleted` column in the table will have the value `True`.)

```python
# Write your query here and figure out the answer
```

```python
deleted_posts = client.query("""
                    SELECT COUNT(1) AS num_deleted_posts
                    FROM `bigquery-public-data.hacker_news.full`
                    WHERE deleted = True
                    """, job_config=safe_config).to_dataframe()
num_deleted_posts = int(deleted_posts.num_deleted_posts.iloc[0])
print(num_deleted_posts)
q_2.check()
```

For the solution, uncomment the line below.

```python
#q_2.solution()
```

# Keep Going
**[Click here](https://www.kaggle.com/dansbecker/order-by)** to move on and learn about the **ORDER BY** clause.

---




*Have questions or comments? Visit the [course discussion forum](https://www.kaggle.com/learn/intro-to-sql/discussion) to chat with other learners.*
