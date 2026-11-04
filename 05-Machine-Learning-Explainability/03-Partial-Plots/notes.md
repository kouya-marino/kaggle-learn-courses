# Partial Plots

*Machine Learning Explainability — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/partial-plots) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-partial-plots)

## Key ideas

- Partial dependence plots show how predictions change as one feature changes, others held fixed.
- 2D plots reveal interactions; `PartialDependenceDisplay.from_estimator`.

## Functions and tools used

`pd.read_csv`, `train_test_split`, `.fit`, `DecisionTreeClassifier`, `.export_graphviz`, `.Source`, `.from_estimator`, `plt.show`, `RandomForestClassifier`, `plt.subplots`

## Exercise

### `q_1` — Question 1

**Discussion:** The code is

    for feat_name in base_features:
        PartialDependenceDisplay.from_estimator(first_model, val_X, [feat_name])
        plt.show()


We have a sense from the permutation importance results that distance is the most important determinant of taxi fare.

This model didn't include distance measures (like absolute change in latitude or longitude) as features, so coordinate features (like `pickup_longitude`) capture the effect of distance.
Being picked up near the center of the longitude values lowers predicted fares on average, because it means shorter trips (on average).

For the same reason, we see the general U-shape in all our partial dependence plots.

### `q_2` — Question 2

**Discussion:** You should expect the plot to have contours running along a diagonal. We see that to some extent, though there are interesting caveats.

We expect the diagonal contours because these are pairs of values where the pickup and dropoff longitudes are nearby, indicating shorter trips (controlling for other factors).

As you get further from the central diagonal, we should expect prices to increase as the distances between the pickup and dropoff longitudes also increase.

The surprising feature is that prices increase as you go further to the upper-right of this graph, even staying near that 45-degree line.

This could be worth further investigation, though the effect of moving to the upper right of this graph is small compared to moving away from that 45-degree line.

The code you need to create the desired plot is:

    fig, ax = plt.subplots(figsize=(8, 6))
    fnames = [('pickup_longitude', 'dropoff_longitude')]
    disp = PartialDependenceDisplay.from_estimator(first_model, val_X, fnames, ax=ax)
    plt.show()

### `q_3` — Question 3

**My answer:**

```python
savings_from_shorter_trip = 6
```

### `q_4` — Question 4

**My answer:**

```python
data['abs_lon_change'] = abs(data.dropoff_longitude - data.pickup_longitude)
data['abs_lat_change'] = abs(data.dropoff_latitude - data.pickup_latitude)
features_2 = ['pickup_longitude', 'pickup_latitude', 'dropoff_longitude', 'dropoff_latitude', 'abs_lat_change', 'abs_lon_change']
X = data[features_2]
new_train_X, new_val_X, new_train_y, new_val_y = train_test_split(X, y, random_state=1)
second_model = RandomForestRegressor(n_estimators=30, random_state=1).fit(new_train_X, new_train_y)
disp = PartialDependenceDisplay.from_estimator(second_model, new_val_X, ['pickup_longitude'])
```

### `q_5` — Question 5

**Discussion:** No. This doesn't guarantee `feat_a` is more important. For example, `feat_a` could have a big effect in the cases where it varies, but could have a single value 99\% of the time. In that case, permuting `feat_a` wouldn't matter much, since most values would be unchanged.

### `q_6` — Question 6

**My answer:**

```python
n_samples = 20000
X1 = 4 * rand(n_samples) - 2
X2 = 4 * rand(n_samples) - 2
y = -2 * X1 * (X1 < -1) + X1 - 2 * X1 * (X1 > 1) - X2
my_df = pd.DataFrame({'X1': X1, 'X2': X2, 'y': y})
predictors_df = my_df.drop(['y'], axis=1)
my_model = RandomForestRegressor(n_estimators=30, random_state=1).fit(predictors_df, my_df.y)
disp = PartialDependenceDisplay.from_estimator(my_model, predictors_df, ['X1'])
```

### `q_7` — Question 7

**My answer:**

```python
import eli5
from eli5.sklearn import PermutationImportance
X1 = 4 * rand(n_samples) - 2
X2 = 4 * rand(n_samples) - 2
y = X1 * X2
my_df = pd.DataFrame({'X1': X1, 'X2': X2, 'y': y})
predictors_df = my_df.drop(['y'], axis=1)
my_model = RandomForestRegressor(n_estimators=30, random_state=1).fit(predictors_df, my_df.y)
disp = PartialDependenceDisplay.from_estimator(my_model, predictors_df, ['X1'], grid_resolution=300)
perm = PermutationImportance(my_model).fit(predictors_df, my_df.y)
```
