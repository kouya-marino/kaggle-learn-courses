# Summary Functions and Maps

*Pandas — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/residentmario/summary-functions-and-maps) · [Exercise on Kaggle](https://www.kaggle.com/code/residentmario/exercise-summary-functions-and-maps)

## Key ideas

- Summary functions: `describe()`, `mean()`, `median()`, `unique()`, `value_counts()`.
- `Series.map()` transforms values one by one; `DataFrame.apply(axis='columns')` works row by row.
- Plain vectorised arithmetic (e.g. `s - s.mean()`) is simpler and faster than `map`.

## Functions and tools used

`pd.set_option`, `pd.read_csv`, `.describe`, `.mean`, `.unique`, `.value_counts`, `.map`, `.apply`, `.head`

## Exercise

### `q1` — 1. What is the median of the `points` column in the `reviews` DataFrame?

**My answer:**

```python
median_points = reviews.points.median()
```

### `q2` — 2. What countries are represented in the dataset? (Your answer should not include any duplicates.)

**My answer:**

```python
countries = reviews.country.unique()
```

### `q3` — 3. How often does each country appear in the dataset? Create a Series `reviews_per_country` mapping countries to the count of reviews of win

**My answer:**

```python
reviews_per_country = reviews.country.value_counts()
```

### `q4` — 4. Create variable `centered_price` containing a version of the `price` column with the mean price subtracted.

**My answer:**

```python
centered_price = reviews.price - reviews.price.mean()
```

### `q5` — 5. I'm an economical wine buyer. Which wine is the "best bargain"? Create a variable `bargain_wine` with the title of the wine with the high

**My answer:**

```python
bargain_idx = (reviews.points / reviews.price).idxmax()
bargain_wine = reviews.loc[bargain_idx, 'title']
```

### `q6` — 6. There are only so many words you can use when describing a bottle of wine. Is a wine more likely to be "tropical" or "fruity"? Create a S

**My answer:**

```python
n_trop = reviews.description.map(lambda desc: "tropical" in desc).sum()
n_fruity = reviews.description.map(lambda desc: "fruity" in desc).sum()
descriptor_counts = pd.Series([n_trop, n_fruity], index=['tropical', 'fruity'])
```

### `q7` — 7. We'd like to host these wine reviews on our website, but a rating system ranging from 80 to 100 points is too hard to understand - we'd l

**My answer:**

```python
def stars(row):
    if row.country == 'Canada':
        return 3
    elif row.points >= 95:
        return 3
    elif row.points >= 85:
        return 2
    else:
        return 1
star_ratings = reviews.apply(stars, axis='columns')
```
