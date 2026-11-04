# Joining Data

*Intro to SQL — lesson 6* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/joining-data) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-joining-data)

## Key ideas

- `INNER JOIN ... ON` combines tables on a shared key; table aliases keep queries short.
- Joining questions and answers finds experts for a topic.

## Functions and tools used

`bigquery.Client`, `client.dataset`, `client.get_dataset`, `.table`, `client.get_table`, `.to_dataframe`, `client.list_rows`, `bigquery.QueryJobConfig`, `client.query`

## Exercise

### `q_1` — 1) Explore the data

**My answer:**

```python
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)
list_of_tables = [t.table_id for t in client.list_tables(dataset)]
print(list_of_tables)
```

### `q_2` — 2) Review relevant tables

**Discussion:** `posts_questions` has a column called `tags` which lists the topics/technologies each question is about.

`posts_answers` has a column called `parent_id` which identifies the ID of the question each answer is responding to.
`posts_answers` also has an `owner_user_id` column which specifies the ID of the user who answered the question.

You can join these two tables to:
- determine the `tags` for each answer, and then
- select the `owner_user_id` of the answers on the desired tag.

This is exactly what you will do over the next few questions.

### `q_3` — 3) Selecting the right questions

**My answer:**

```python
questions_query = """
                  SELECT id, title, owner_user_id
                  FROM `bigquery-public-data.stackoverflow.posts_questions`
                  WHERE tags LIKE '%bigquery%'
                  """
questions_query_job = client.query(questions_query, job_config=safe_config)
questions_results = questions_query_job.to_dataframe()
print(questions_results.head())
```

### `q_4` — 4) Your first join

**My answer:**

```python
answers_query = """
                SELECT a.id, a.body, a.owner_user_id
                FROM `bigquery-public-data.stackoverflow.posts_questions` AS q
                INNER JOIN `bigquery-public-data.stackoverflow.posts_answers` AS a
                    ON q.id = a.parent_id
                WHERE q.tags LIKE '%bigquery%'
                """
answers_query_job = client.query(answers_query, job_config=bigquery.QueryJobConfig(maximum_bytes_billed=27*10**10))
answers_results = answers_query_job.to_dataframe()
print(answers_results.head())
```

### `q_5` — 5) Answer the question

**My answer:**

```python
bigquery_experts_query = """
                         SELECT a.owner_user_id AS user_id, COUNT(1) AS number_of_answers
                         FROM `bigquery-public-data.stackoverflow.posts_questions` AS q
                         INNER JOIN `bigquery-public-data.stackoverflow.posts_answers` AS a
                             ON q.id = a.parent_Id
                         WHERE q.tags LIKE '%bigquery%'
                         GROUP BY a.owner_user_id
                         """
bigquery_experts_query_job = client.query(bigquery_experts_query, job_config=safe_config)
bigquery_experts_results = bigquery_experts_query_job.to_dataframe()
print(bigquery_experts_results.head())
```

### `q_6` — 6) Building a more generally useful service

**Discussion:** def expert_finder(topic, client):
    '''
    Returns a DataFrame with the user IDs who have written Stack Overflow answers on a topic.

    Inputs:
        topic: A string with the topic of interest
        client: A Client object that specifies the connection to the Stack Overflow dataset

    Outputs:
        results: A DataFrame with columns for user_id and number_of_answers. Follows similar logic to bigquery_experts_results shown above.
    '''
    my_query = """
               SELECT a.owner_user_id AS user_id, COUNT(1) AS number_of_answers
               FROM `bigquery-public-data.stackoverflow.posts_questions` AS q
               INNER JOIN `bigquery-public-data.stackoverflow.posts_answers` AS a
                   ON q.id = a.parent_Id
               WHERE q.tags like '%{topic}%'
               GROUP BY a.owner_user_id
               """
               
    # Set up the query (a real service would have good error handling for 
    # queries that scan too much data)
    safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=10**10)      
    my_query_job = client.query(my_query, job_config=safe_config)
    
    # API request - run the query, and return a pandas DataFrame
    results = my_query_job.to_dataframe()

    return results
