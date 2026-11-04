# Exercise: Getting Started With SQL and BigQuery


**This notebook is an exercise in the [SQL](https://www.kaggle.com/learn/intro-to-sql) course.  You can reference the tutorial at [this link](https://www.kaggle.com/dansbecker/getting-started-with-sql-and-bigquery).**

---

# Introduction

The first test of your new data exploration skills uses data describing crime in the city of Chicago.

Before you get started, run the following cell. It sets up the automated feedback system to review your answers.

```python
# Set up feedack system
from learntools.core import binder
binder.bind(globals())
from learntools.sql.ex1 import *
print("Setup Complete")
```

Use the next code cell to fetch the dataset.

```python
from google.cloud import bigquery

# Create a "Client" object
client = bigquery.Client()

# Construct a reference to the "chicago_crime" dataset
dataset_ref = client.dataset("chicago_crime", project="bigquery-public-data")

# API request - fetch the dataset
dataset = client.get_dataset(dataset_ref)
```

# Exercises

### 1) Count tables in the dataset

How many tables are in the Chicago Crime dataset?

```python
# Write the code you need here to figure out the answer
```

```python
num_tables = ____  # Store the answer as num_tables and then run this cell

# Check your answer
q_1.check()
```

For a hint or the solution, uncomment the appropriate line below.

```python
#q_1.hint()
#q_1.solution()
```

### 2) Explore the table schema

How many columns in the `crime` table have `TIMESTAMP` data?

```python
# Write the code to figure out the answer
```

```python
num_timestamp_fields = ____ # Put your answer here

# Check your answer
q_2.check()
```

For a hint or the solution, uncomment the appropriate line below.

```python
#q_2.hint()
#q_2.solution()
```

### 3) Create a crime map

If you wanted to create a map with a dot at the location of each crime, what are the names of the two fields you likely need to pull out of the `crime` table to plot the crimes on a map?

```python
# Write the code here to explore the data so you can find the answer
```

```python
fields_for_plotting = [____, ____] # Put your answers here

# Check your answer
q_3.check()
```

For a hint or the solution, uncomment the appropriate line below.

```python
#q_3.hint()
#q_3.solution()
```

Thinking about the question above, there are a few columns that appear to have geographic data. Look at a few values (with the `list_rows()` command) to see if you can determine their relationship.  Two columns will still be hard to interpret. But it should be obvious how the `location` column relates to `latitude` and `longitude`.

```python
# Scratch space for your code
```

# Keep going

You've looked at the schema, but you haven't yet done anything exciting with the data itself. Things get more interesting when you get to the data, so keep going to **[write your first SQL query](https://www.kaggle.com/dansbecker/select-from-where).**

---




*Have questions or comments? Visit the [course discussion forum](https://www.kaggle.com/learn/intro-to-sql/discussion) to chat with other learners.*
