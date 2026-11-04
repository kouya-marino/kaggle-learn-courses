# Exercise: Group By, Having & Count


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
# Query to select prolific commenters and post counts
prolific_commenters_query = """____""" # Your code goes here

# Set up the query (cancel the query if it would use too much of 
# your quota, with the limit set to 1 GB)
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
query_job = client.query(prolific_commenters_query, job_config=safe_config)

# API request - run the query, and return a pandas DataFrame
prolific_commenters = query_job.to_dataframe()

# View top few rows of results
print(prolific_commenters.head())

# Check your answer
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
num_deleted_posts = ____ # Put your answer here

# Check your answer
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
