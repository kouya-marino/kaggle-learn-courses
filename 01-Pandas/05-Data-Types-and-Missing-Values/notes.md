# Data Types and Missing Values

*Pandas — lesson 5* · [Tutorial on Kaggle](https://www.kaggle.com/code/residentmario/data-types-and-missing-values) · [Exercise on Kaggle](https://www.kaggle.com/code/residentmario/exercise-data-types-and-missing-values)

## Key ideas

- `dtype` / `dtypes` show column types; `astype()` converts them.
- Missing entries are `NaN`; find them with `isnull()` / `notnull()`.
- `fillna()` and `replace()` fill or fix values.

## Functions and tools used

`pd.read_csv`, `pd.set_option`, `.astype`, `pd.isnull`, `.fillna`, `.replace`

## Exercise

### `q1` — 1. What is the data type of the `points` column in the dataset?

**My answer:**

```python
dtype = reviews.points.dtype
```

### `q2` — 2. Create a Series from entries in the `points` column, but convert the entries to strings. Hint: strings are `str` in native Python.

**My answer:**

```python
point_strings = reviews.points.astype(str)
```

### `q3` — 3. Sometimes the price column is null. How many reviews in the dataset are missing a price?

**My answer:**

```python
n_missing_prices = reviews.price.isnull().sum()
```

### `q4` — 4. What are the most common wine-producing regions? Create a Series counting the number of times each value occurs in the `region_1` field. 

**My answer:**

```python
reviews_per_region = reviews.region_1.fillna('Unknown').value_counts().sort_values(ascending=False)
```
