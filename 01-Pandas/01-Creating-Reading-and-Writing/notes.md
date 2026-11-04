# Creating, Reading and Writing

*Pandas — lesson 1* · [Tutorial on Kaggle](https://www.kaggle.com/code/residentmario/creating-reading-and-writing) · [Exercise on Kaggle](https://www.kaggle.com/code/residentmario/exercise-creating-reading-and-writing)

## Key ideas

- A `DataFrame` is a table; a `Series` is a single column (a list with an index).
- Build them from dicts or lists, and set row labels with `index=`.
- `pd.read_csv(path, index_col=0)` loads a file; `.shape` and `.head()` give a first look; `.to_csv()` writes one back.

## Functions and tools used

`pd.DataFrame`, `pd.Series`, `pd.read_csv`, `.head`

## Exercise

### `q1` — 1. In the cell below, create a DataFrame `fruits` that looks like this:

**My answer:**

```python
fruits = pd.DataFrame([[30, 21]], columns=['Apples', 'Bananas'])
```

### `q2` — 2. Create a dataframe `fruit_sales` that matches the diagram below:

**My answer:**

```python
fruit_sales = pd.DataFrame([[35, 21], [41, 34]], columns=['Apples', 'Bananas'], index=['2017 Sales', '2018 Sales'])
```

### `q3` — 3. Create a variable `ingredients` with a Series that looks like:

**My answer:**

```python
ingredients = pd.Series(['4 cups', '1 cup', '2 large', '1 can'], index=['Flour', 'Milk', 'Eggs', 'Spam'], name='Dinner')
```

### `q4` — 4. Read the following csv dataset of wine reviews into a DataFrame called `reviews`:

**My answer:**

```python
reviews = pd.read_csv('../input/wine-reviews/winemag-data_first150k.csv', index_col=0)
```

### `q5` — 5. Run the cell below to create and display a DataFrame called `animals`:

**Answer:**

```python
animals.to_csv("cows_and_goats.csv")
```

### `q6`

**Answer:**

```python
import sqlite3
conn = sqlite3.connect("../input/pitchfork-data/database.sqlite")

music_reviews = pd.read_sql_query("SELECT * FROM artists", conn)
```
