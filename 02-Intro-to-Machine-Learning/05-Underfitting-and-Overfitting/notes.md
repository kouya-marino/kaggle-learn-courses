# Underfitting and Overfitting

*Intro to Machine Learning — lesson 5* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/underfitting-and-overfitting) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-underfitting-and-overfitting)

## Key ideas

- Shallow trees underfit, very deep trees overfit.
- `max_leaf_nodes` controls tree size; pick the value with the lowest validation MAE.
- Refit the final model on all the data once the size is chosen.

## Functions and tools used

`DecisionTreeRegressor`, `.fit`, `.predict`, `mean_absolute_error`, `pd.read_csv`, `.dropna`, `train_test_split`, `get_mae`

## Exercise

### `step_1` — Step 1: Compare Different Tree Sizes

**My answer:**

```python
candidate_max_leaf_nodes = [5, 25, 50, 100, 250, 500]
scores = {leaf_size: get_mae(leaf_size, train_X, val_X, train_y, val_y) for leaf_size in candidate_max_leaf_nodes}
best_tree_size = min(scores, key=scores.get)
print(scores, best_tree_size)
```

### `step_2` — Step 2: Fit Model Using All Data

**Answer:**

```python
# Fit the model with best_tree_size. Fill in argument to make optimal size
final_model = DecisionTreeRegressor(max_leaf_nodes=best_tree_size, random_state=1)

# fit the final model
final_model.fit(X, y)
```
