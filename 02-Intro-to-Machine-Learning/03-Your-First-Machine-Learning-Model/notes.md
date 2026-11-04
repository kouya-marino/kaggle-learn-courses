# Your First Machine Learning Model

*Intro to Machine Learning — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/your-first-machine-learning-model) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-your-first-machine-learning-model)

## Key ideas

- Choose a target `y` and a feature matrix `X`.
- The scikit-learn workflow is define → fit → predict → evaluate.
- Set `random_state` so results are reproducible.

## Functions and tools used

`pd.read_csv`, `.dropna`, `.describe`, `.head`, `DecisionTreeRegressor`, `.fit`, `.predict`

## Exercise

### `step_1` — Step 1: Specify Prediction Target

**My answer:**

```python
from sklearn.tree import DecisionTreeRegressor
y = home_data.SalePrice
```

### `step_2` — Step 2: Create X

**My answer:**

```python
feature_names = ["LotArea", "YearBuilt", "1stFlrSF", "2ndFlrSF", "FullBath", "BedroomAbvGr", "TotRmsAbvGrd"]
X = home_data[feature_names]
```

### `step_3` — Step 3: Specify and Fit Model

**My answer:**

```python
iowa_model = DecisionTreeRegressor(random_state=1)
iowa_model.fit(X, y)
```

### `step_4` — Step 4: Make Predictions

**My answer:**

```python
predictions = iowa_model.predict(X)
print(predictions)
```
