# Cross-Validation

*Intermediate Machine Learning — lesson 5* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/cross-validation) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-cross-validation)

## Key ideas

- k-fold cross-validation gives a more reliable estimate than one split, especially on small data.
- `cross_val_score` works directly with a pipeline (`scoring='neg_mean_absolute_error'`).
- Use it to tune parameters such as `n_estimators`.

## Functions and tools used

`pd.read_csv`, `Pipeline`, `SimpleImputer`, `RandomForestRegressor`, `cross_val_score`, `.mean`

## Exercise

### `step_1` — Step 1: Write a useful function

**My answer:**

```python
def get_score(n_estimators):
    my_pipeline = Pipeline(steps=[
        ('preprocessor', SimpleImputer()),
        ('model', RandomForestRegressor(n_estimators, random_state=0))
    ])
    scores = -1 * cross_val_score(my_pipeline, X, y, cv=3, scoring='neg_mean_absolute_error')
    return scores.mean()
```

### `step_2` — Step 2: Test different parameter values

**My answer:**

```python
results = {50 * i: get_score(50 * i) for i in range(1, 9)}
print(results)
```

### `step_3` — Step 3: Find the best parameter value

**My answer:**

```python
n_estimators_best = min(results, key=results.get)
```
