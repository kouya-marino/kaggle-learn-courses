# Indexing, Selecting & Assigning

*Pandas — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/residentmario/indexing-selecting-assigning) · [Exercise on Kaggle](https://www.kaggle.com/code/residentmario/exercise-indexing-selecting-assigning)

## Key ideas

- Columns can be read as attributes (`df.col`) or with `df['col']`.
- `iloc` selects by position (end excluded); `loc` selects by label (end included).
- Conditional selection combines boolean masks with `&` / `|`, plus helpers like `isin()` and `notnull()`.

## Functions and tools used

`pd.read_csv`, `pd.set_option`, `.set_index`, `.isin`, `.notnull`

## Exercise

### `q1` — 1. Select the `description` column from `reviews` and assign the result to the variable `desc`.

**My answer:**

```python
desc = reviews.description
```

### `q2` — 2. Select the first value from the description column of `reviews`, assigning it to variable `first_description`.

**My answer:**

```python
first_description = reviews.description.iloc[0]
```

### `q3` — 3. Select the first row of data (the first record) from `reviews`, assigning it to the variable `first_row`.

**My answer:**

```python
first_row = reviews.iloc[0]
```

### `q4` — 4. Select the first 10 values from the `description` column in `reviews`, assigning the result to variable `first_descriptions`.

**My answer:**

```python
first_descriptions = reviews.description.iloc[:10]
```

### `q5` — 5. Select the records with index labels `1`, `2`, `3`, `5`, and `8`, assigning the result to the variable `sample_reviews`.

**My answer:**

```python
sample_reviews = reviews.loc[[1, 2, 3, 5, 8]]
```

### `q6` — 6. Create a variable `df` containing the `country`, `province`, `region_1`, and `region_2` columns of the records with the index labels `0`,

**My answer:**

```python
df = reviews.loc[[0, 1, 10, 100], ['country', 'province', 'region_1', 'region_2']]
```

### `q7` — 7. Create a variable `df` containing the `country` and `variety` columns of the first 100 records.

**My answer:**

```python
df = reviews.loc[:99, ['country', 'variety']]
```

### `q8` — 8. Create a DataFrame `italian_wines` containing reviews of wines made in `Italy`. Hint: `reviews.country` equals what?

**My answer:**

```python
italian_wines = reviews[reviews.country == 'Italy']
```

### `q9` — 9. Create a DataFrame `top_oceania_wines` containing all reviews with at least 95 points (out of 100) for wines from Australia or New Zealan

**My answer:**

```python
top_oceania_wines = reviews.loc[(reviews.country.isin(['Australia', 'New Zealand'])) & (reviews.points >= 95)]
```
