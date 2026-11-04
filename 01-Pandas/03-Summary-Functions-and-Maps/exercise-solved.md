# Exercise (solved): Summary Functions and Maps


**This notebook is an exercise in the [Pandas](https://www.kaggle.com/learn/pandas) course.  You can reference the tutorial at [this link](https://www.kaggle.com/residentmario/summary-functions-and-maps).**

---

# Introduction

Now you are ready to get a deeper understanding of your data.

Run the following cell to load your data and some utility functions (including code to check your answers).

```python
import pandas as pd
pd.set_option("display.max_rows", 5)
reviews = pd.read_csv("../input/wine-reviews/winemag-data-130k-v2.csv", index_col=0)

from learntools.core import binder; binder.bind(globals())
from learntools.pandas.summary_functions_and_maps import *
print("Setup complete.")

reviews.head()
```

# Exercises

## 1.

What is the median of the `points` column in the `reviews` DataFrame?

```python
median_points = reviews.points.median()
q1.check()
```

```python
#q1.hint()
#q1.solution()
```

## 2. 
What countries are represented in the dataset? (Your answer should not include any duplicates.)

```python
countries = reviews.country.unique()
q2.check()
```

```python
#q2.hint()
#q2.solution()
```

## 3.
How often does each country appear in the dataset? Create a Series `reviews_per_country` mapping countries to the count of reviews of wines from that country.

```python
reviews_per_country = reviews.country.value_counts()
q3.check()
```

```python
#q3.hint()
#q3.solution()
```

## 4.
Create variable `centered_price` containing a version of the `price` column with the mean price subtracted.

(Note: this 'centering' transformation is a common preprocessing step before applying various machine learning algorithms.)

```python
centered_price = reviews.price - reviews.price.mean()
q4.check()
```

```python
#q4.hint()
#q4.solution()
```

## 5.
I'm an economical wine buyer. Which wine is the "best bargain"? Create a variable `bargain_wine` with the title of the wine with the highest points-to-price ratio in the dataset.

```python
bargain_idx = (reviews.points / reviews.price).idxmax()
bargain_wine = reviews.loc[bargain_idx, 'title']
q5.check()
```

```python
#q5.hint()
#q5.solution()
```

## 6.
There are only so many words you can use when describing a bottle of wine. Is a wine more likely to be "tropical" or "fruity"? Create a Series `descriptor_counts` counting how many times each of these two words appears in the `description` column in the dataset. (For simplicity, let's ignore the capitalized versions of these words.)

```python
n_trop = reviews.description.map(lambda desc: "tropical" in desc).sum()
n_fruity = reviews.description.map(lambda desc: "fruity" in desc).sum()
descriptor_counts = pd.Series([n_trop, n_fruity], index=['tropical', 'fruity'])
q6.check()
```

```python
#q6.hint()
#q6.solution()
```

## 7.
We'd like to host these wine reviews on our website, but a rating system ranging from 80 to 100 points is too hard to understand - we'd like to translate them into simple star ratings. A score of 95 or higher counts as 3 stars, a score of at least 85 but less than 95 is 2 stars. Any other score is 1 star.

Also, the Canadian Vintners Association bought a lot of ads on the site, so any wines from Canada should automatically get 3 stars, regardless of points.

Create a series `star_ratings` with the number of stars corresponding to each review in the dataset.

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
q7.check()
```

```python
#q7.hint()
#q7.solution()
```

# Keep going
Continue to **[grouping and sorting](https://www.kaggle.com/residentmario/grouping-and-sorting)**.

---




*Have questions or comments? Visit the [course discussion forum](https://www.kaggle.com/learn/pandas/discussion) to chat with other learners.*
