# Renaming and Combining

*Pandas — lesson 6* · [Tutorial on Kaggle](https://www.kaggle.com/code/residentmario/renaming-and-combining) · [Exercise on Kaggle](https://www.kaggle.com/code/residentmario/exercise-renaming-and-combining)

## Key ideas

- `rename(columns=...)` and `rename_axis()` change column / index names.
- `pd.concat([...])` stacks frames that share columns.
- `join()` combines frames on their index — set the key with `set_index()` first.

## Functions and tools used

`pd.set_option`, `pd.read_csv`, `.rename`, `.rename_axis`, `pd.concat`, `.set_index`, `.join`

## Exercise

### `q1` — 1. `region_1` and `region_2` are pretty uninformative names for locale columns in the dataset. Create a copy of `reviews` with these columns

**My answer:**

```python
renamed = reviews.rename(columns=dict(region_1='region', region_2='locale'))
```

### `q2` — 2. Set the index name in the dataset to `wines`.

**My answer:**

```python
reindexed = reviews.rename_axis('wines', axis='rows')
```

### `q3` — 3. The [Things on Reddit](https://www.kaggle.com/residentmario/things-on-reddit/data) dataset includes product links from a selection of top

**My answer:**

```python
combined_products = pd.concat([gaming_products, movie_products])
```

### `q4` — 4. The [Powerlifting Database](https://www.kaggle.com/open-powerlifting/powerlifting-database) dataset on Kaggle includes one CSV table for 

**My answer:**

```python
powerlifting_combined = powerlifting_meets.set_index("MeetID").join(powerlifting_competitors.set_index("MeetID"))
```
