# Random Forests

*Intro to Machine Learning — lesson 6* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/random-forests) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-random-forests)

## Key ideas

- A random forest averages many trees and usually beats a single tree with default settings.
- `RandomForestRegressor` works well with little tuning.

## Functions and tools used

`pd.read_csv`, `.dropna`, `train_test_split`, `RandomForestRegressor`, `.fit`, `.predict`, `mean_absolute_error`

## Exercise

### `step_1` — Step 1: Use a Random Forest

**My answer:**

```python
from sklearn.ensemble import RandomForestRegressor
rf_model = RandomForestRegressor(random_state=1)
rf_model.fit(train_X, train_y)
rf_val_mae = mean_absolute_error(rf_model.predict(val_X), val_y)
print("Validation MAE for Random Forest Model: {}".format(rf_val_mae))
```
