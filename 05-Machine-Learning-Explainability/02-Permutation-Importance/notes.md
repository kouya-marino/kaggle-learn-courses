# Permutation Importance

*Machine Learning Explainability — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/permutation-importance) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-permutation-importance)

## Key ideas

- Permutation importance: shuffle one feature in the validation data and measure how much the score drops.
- Model-agnostic and fast; `eli5`'s `PermutationImportance`.

## Functions and tools used

`pd.read_csv`, `train_test_split`, `.fit`, `RandomForestClassifier`, `eli5.show_weights`, `PermutationImportance`, `.tolist`

## Exercise

### `q_1` — Question 1

**Discussion:** It would be helpful to know whether New York City taxis
    vary prices based on how many passengers they have. Most places do not
    change fares based on numbers of passengers.
    If you assume New York City is the same, then only the top 4 features listed should matter. At first glance, it seems all of those should matter equally.

### `q_2` — Question 2

**My answer:**

```python
perm = PermutationImportance(first_model, random_state=1).fit(val_X, val_y)
```

### `q_3` — Question 3

**Discussion:** 1. Travel might tend to have greater latitude distances than longitude distances. If the longitudes values were generally closer together, shuffling them wouldn't matter as much.
    2. Different parts of the city might have different pricing rules (e.g. price per mile), and pricing rules could vary more by latitude than longitude.
    3. Tolls might be greater on roads going North<->South (changing latitude) than on roads going East <-> West (changing longitude).  Thus latitude would have a larger effect on the prediction because it captures the amount of the tolls.

### `q_4` — Question 4

**My answer:**

```python
data['abs_lon_change'] = abs(data.dropoff_longitude - data.pickup_longitude)
data['abs_lat_change'] = abs(data.dropoff_latitude - data.pickup_latitude)
features_2 = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude', 'dropoff_latitude', 'abs_lat_change', 'abs_lon_change']
X = data[features_2]
new_train_X, new_val_X, new_train_y, new_val_y = train_test_split(X, y, random_state=1)
second_model = RandomForestRegressor(n_estimators=30, random_state=1).fit(new_train_X, new_train_y)
perm2 = PermutationImportance(second_model, random_state=1).fit(new_val_X, new_val_y)
```

### `q_5` — Question 5

**Discussion:** The scale of features does not affect permutation importance per se. The only reason that rescaling a feature would affect PI is indirectly, if rescaling helped or hurt the ability of the particular learning method we're using to make use of that feature.
    That won't happen with tree based models, like the Random Forest used here.
    If you are familiar with Ridge Regression, you might be able to think of how that would be affected.
    That said, the absolute change features are have high importance because they capture total distance traveled, which is the primary determinant of taxi fares...It is not an artifact of the feature magnitude.

### `q_6` — Question 6

**Discussion:** We cannot tell from the permutation importance results whether traveling a fixed latitudinal distance is more or less expensive than traveling the same longitudinal distance.
    Possible reasons latitude feature are more important than longitude features
    1. latitudinal distances in the dataset tend to be larger
    2. it is more expensive to travel a fixed latitudinal distance
    3. Both of the above
    If abs_lon_change values were very small, longitues could be less important to the model even if the cost per mile of travel in that direction were high.
