# Model Validation

*Intro to Machine Learning — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/model-validation) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-model-validation)

## Key ideas

- Scoring on the training data is misleading (in-sample error).
- Mean absolute error (MAE) is an easy-to-read metric.
- `train_test_split` holds back validation data for honest scores.

## Functions and tools used

`pd.read_csv`, `.dropna`, `DecisionTreeRegressor`, `.fit`, `.predict`, `mean_absolute_error`, `train_test_split`

## Exercise

### `step_1` — Step 1: Split Your Data

**Answer:**

```python
from sklearn.model_selection import train_test_split
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state=1)
```

### `step_2` — Step 2: Specify and Fit the Model

**My answer:**

```python
iowa_model = DecisionTreeRegressor(random_state=1)
iowa_model.fit(train_X, train_y)
```

### `step_3` — Step 3: Make Predictions with Validation data

**My answer:**

```python
val_predictions = iowa_model.predict(val_X)
```

### `step_4` — Step 4: Calculate the Mean Absolute Error in Validation Data

**My answer:**

```python
print(val_predictions[:5])
print(val_y.head().tolist())
val_mae = mean_absolute_error(val_y, val_predictions)
print(val_mae)
```
