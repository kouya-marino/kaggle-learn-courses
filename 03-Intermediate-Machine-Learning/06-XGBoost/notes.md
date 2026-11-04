# XGBoost

*Intermediate Machine Learning — lesson 6* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/xgboost) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-xgboost)

## Key ideas

- Gradient boosting adds trees one after another, each correcting the previous errors.
- Key XGBoost parameters: `n_estimators`, `learning_rate`, early stopping, `n_jobs`.

## Functions and tools used

`pd.read_csv`, `train_test_split`, `XGBRegressor`, `.fit`, `.predict`, `mean_absolute_error`

## Exercise

### `step_1.a` — Step 1: Build model — Part A

**My answer:**

```python
from sklearn.metrics import mean_absolute_error
from xgboost import XGBRegressor
my_model_1 = XGBRegressor(random_state=0)
my_model_1.fit(X_train, y_train)
```

### `step_1.b` — Step 1: Build model — Part B

**My answer:**

```python
predictions_1 = my_model_1.predict(X_valid)
```

### `step_1.c` — Step 1: Build model — Part C

**My answer:**

```python
mae_1 = mean_absolute_error(predictions_1, y_valid)
print("MAE 1:", mae_1)
```

### `step_2` — Step 2: Improve the model

**My answer:**

```python
my_model_2 = XGBRegressor(n_estimators=1000, learning_rate=0.05)
my_model_2.fit(X_train, y_train)
predictions_2 = my_model_2.predict(X_valid)
mae_2 = mean_absolute_error(predictions_2, y_valid)
print("MAE 2:", mae_2)
```

### `step_3` — Step 3: Break the model

**My answer:**

```python
my_model_3 = XGBRegressor(n_estimators=1)
my_model_3.fit(X_train, y_train)
predictions_3 = my_model_3.predict(X_valid)
mae_3 = mean_absolute_error(predictions_3, y_valid)
print("MAE 3:", mae_3)
```
