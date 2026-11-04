# Introduction

*Intermediate Machine Learning — lesson 1* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/introduction) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-introduction)

## Key ideas

- Compare several model configurations by validation MAE and keep the best.
- A recap of the define / fit / predict / score workflow on the housing data.

## Exercise

### `step_1` — Step 1: Evaluate several models

**My answer:**

```python
for i, m in enumerate(models):
    m.fit(X_train, y_train)
    print("Model %d MAE: %d" % (i + 1, mean_absolute_error(y_valid, m.predict(X_valid))))
best_model = model_3
```

### `step_2` — Step 2: Generate test predictions

**My answer:**

```python
my_model = RandomForestRegressor(n_estimators=100, criterion='absolute_error', random_state=0)
```
