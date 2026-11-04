# Grouping and Sorting

*Pandas — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/residentmario/grouping-and-sorting) · [Exercise on Kaggle](https://www.kaggle.com/code/residentmario/exercise-grouping-and-sorting)

## Key ideas

- `groupby()` + `size()`, `count()`, `max()` or `agg([...])` summarises each group.
- Grouping on several columns gives a MultiIndex; `reset_index()` flattens it.
- `sort_values(by=..., ascending=False)` and `sort_index()` order the results.

## Functions and tools used

`pd.read_csv`, `pd.set_option`, `.count`, `.groupby`, `.apply`, `.idxmax`, `.agg`, `.reset_index`, `.sort_values`, `.sort_index`

## Exercise

### `q1` — 1. Who are the most common wine reviewers in the dataset? Create a `Series` whose index is the `taster_twitter_handle` category from the dat

**My answer:**

```python
reviews_written = reviews.groupby('taster_twitter_handle').size()
```

### `q2` — 2. What is the best wine I can buy for a given amount of money? Create a `Series` whose index is wine prices and whose values is the maximum

**My answer:**

```python
best_rating_per_price = reviews.groupby('price')['points'].max().sort_index()
```

### `q3` — 3. What are the minimum and maximum prices for each `variety` of wine? Create a `DataFrame` whose index is the `variety` category from the d

**My answer:**

```python
price_extremes = reviews.groupby('variety').price.agg(['min', 'max'])
```

### `q4` — 4. What are the most expensive wine varieties? Create a variable `sorted_varieties` containing a copy of the dataframe from the previous que

**My answer:**

```python
sorted_varieties = price_extremes.sort_values(by=['min', 'max'], ascending=False)
```

### `q5` — 5. Create a `Series` whose index is reviewers and whose values is the average review score given out by that reviewer. Hint: you will need t

**My answer:**

```python
reviewer_mean_ratings = reviews.groupby('taster_name').points.mean()
```

### `q6` — 6. What combination of countries and varieties are most common? Create a `Series` whose index is a `MultiIndex`of `{country, variety}` pairs

**My answer:**

```python
country_variety_counts = reviews.groupby(['country', 'variety']).size().sort_values(ascending=False)
```
