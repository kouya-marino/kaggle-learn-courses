# Missing Values

*Intermediate Machine Learning — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/missing-values) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-missing-values)

## Key ideas

- Three approaches: drop columns with missing values, impute them (`SimpleImputer`), or impute and add a missing-indicator column.
- Fit the imputer on training data only, then transform validation and test data.

## Functions and tools used

`pd.read_csv`, `.drop`, `.select_dtypes`, `train_test_split`, `RandomForestRegressor`, `score_dataset`, `.isnull`, `SimpleImputer`, `pd.DataFrame`, `.fit_transform`, `.transform`, `.copy`

## Exercise

### `step_1.a` — Step 1: Preliminary investigation — Part A

**My answer:**

```python
from sklearn.impute import SimpleImputer
num_rows = 1168
num_cols_with_missing = 3
tot_missing = 212 + 6 + 58
```

### `step_1.b` — Step 1: Preliminary investigation — Part B

**Discussion:** Since there are relatively few missing entries in the data (the column with the greatest percentage of missing values is missing less than 20% of its entries), we can expect that dropping columns is unlikely to yield good results.  This is because we'd be throwing away a lot of valuable data, and so imputation will likely perform better.

### `step_2` — Step 2: Drop columns with missing values

**My answer:**

```python
cols_with_missing = [col for col in X_train.columns if X_train[col].isnull().any()]
reduced_X_train = X_train.drop(cols_with_missing, axis=1)
reduced_X_valid = X_valid.drop(cols_with_missing, axis=1)
```

### `step_3.a` — Step 3: Imputation — Part A

**My answer:**

```python
my_imputer = SimpleImputer()
imputed_X_train = pd.DataFrame(my_imputer.fit_transform(X_train))
imputed_X_valid = pd.DataFrame(my_imputer.transform(X_valid))
imputed_X_train.columns = X_train.columns
imputed_X_valid.columns = X_valid.columns
```

### `step_3.b` — Step 3: Imputation — Part B

**Discussion:** Given that thre are so few missing values in the dataset, we'd expect imputation to perform better than dropping columns entirely.  However, we see that dropping columns performs slightly better!  While this can probably partially be attributed to noise in the dataset, another potential explanation is that the imputation method is not a great match to this dataset.  That is, maybe instead of filling in the mean value, it makes more sense to set every missing value to a value of 0, to fill in the most frequently encountered value, or to use some other method.  For instance, consider the `GarageYrBlt` column (which indicates the year that the garage was built).  It's likely that in some cases, a missing value could indicate a house that does not have a garage.  Does it make more sense to fill in the median value along each column in this case?  Or could we get better results by filling in the minimum value along each column?  It's not quite clear what's best in this case, but perhaps we can rule out some options immediately - for instance, setting missing values in this column to 0 is likely to yield horrible results!

### `step_4.a` — Step 4: Generate test predictions — Part A

**My answer:**

```python
final_imputer = SimpleImputer(strategy='median')
final_X_train = pd.DataFrame(final_imputer.fit_transform(X_train))
final_X_valid = pd.DataFrame(final_imputer.transform(X_valid))
final_X_train.columns = X_train.columns
final_X_valid.columns = X_valid.columns
```

### `step_4.b` — Step 4: Generate test predictions — Part B

**My answer:**

```python
print("MAE (Your approach):", mean_absolute_error(y_valid, model.predict(final_X_valid)))
final_X_test = pd.DataFrame(final_imputer.transform(X_test))
final_X_test.columns = X_test.columns
preds_test = model.predict(final_X_test)
```
