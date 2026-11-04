# Pipelines

*Intermediate Machine Learning — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/pipelines) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-pipelines)

## Key ideas

- `ColumnTransformer` bundles numeric and categorical preprocessing.
- `Pipeline` chains preprocessing with the model, so one `fit` / `predict` call does everything and leakage is avoided.

## Functions and tools used

`pd.read_csv`, `.drop`, `train_test_split`, `.copy`, `.nunique`, `.head`, `SimpleImputer`, `Pipeline`, `ColumnTransformer`, `OneHotEncoder`, `RandomForestRegressor`, `.fit`

## Exercise

### `step_1.a` — Step 1: Improve the performance — Part A

**My answer:**

```python
categorical_transformer = Pipeline(steps=[
    ('imputer', SimpleImputer(strategy='constant')),
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])
```

### `step_1.b` — Step 1: Improve the performance — Part B

**My answer:**

```python
my_pipeline = Pipeline(steps=[('preprocessor', preprocessor), ('model', model)])
my_pipeline.fit(X_train, y_train)
score = mean_absolute_error(y_valid, my_pipeline.predict(X_valid))
print('MAE:', score)
```

### `step_2` — Step 2: Generate test predictions

**My answer:**

```python
preds_test = my_pipeline.predict(X_test)
```
