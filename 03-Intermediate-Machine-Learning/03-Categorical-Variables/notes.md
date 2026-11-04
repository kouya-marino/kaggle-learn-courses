# Categorical Variables

*Intermediate Machine Learning — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/categorical-variables) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-categorical-variables)

## Key ideas

- Categorical columns can be dropped, ordinal-encoded or one-hot encoded.
- Cardinality (number of unique values) decides whether one-hot encoding is practical.
- Columns with categories unseen in training need care (`handle_unknown='ignore'`).

## Functions and tools used

`pd.read_csv`, `.drop`, `train_test_split`, `.copy`, `.any`, `.select_dtypes`, `score_dataset`, `.fit_transform`, `.transform`, `pd.DataFrame`, `pd.concat`, `.astype`

## Exercise

### `step_1` — Step 1: Drop columns with categorical data

**My answer:**

```python
from sklearn.preprocessing import OrdinalEncoder, OneHotEncoder
drop_X_train = X_train.select_dtypes(exclude=['object'])
drop_X_valid = X_valid.select_dtypes(exclude=['object'])
```

### `step_2.a` — Step 2: Ordinal encoding — Part A

**Discussion:** Fitting an ordinal encoder to a column in the training data creates a corresponding integer-valued label for each unique value **that appears in the training data**. In the case that the validation data contains values that don't also appear in the training data, the encoder will throw an error, because these values won't have an integer assigned to them.  Notice that the `'Condition2'` column in the validation data contains the values `'RRAn'` and `'RRNn'`, but these don't appear in the training data -- thus, if we try to use an ordinal encoder with scikit-learn, the code will throw an error.

### `step_2.b` — Step 2: Ordinal encoding — Part B

**My answer:**

```python
label_X_train = X_train.drop(bad_label_cols, axis=1)
label_X_valid = X_valid.drop(bad_label_cols, axis=1)
ordinal_encoder = OrdinalEncoder()
label_X_train[good_label_cols] = ordinal_encoder.fit_transform(X_train[good_label_cols])
label_X_valid[good_label_cols] = ordinal_encoder.transform(X_valid[good_label_cols])
```

### `step_3.a` — Step 3: Investigating cardinality — Part A

**My answer:**

```python
high_cardinality_numcols = 3
num_cols_neighborhood = 25
```

### `step_3.b` — Step 3: Investigating cardinality — Part B

**My answer:**

```python
OH_entries_added = 1e4 * 100 - 1e4
label_entries_added = 0
```

### `step_4` — Step 4: One-hot encoding

**My answer:**

```python
OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse_output=False)
OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[low_cardinality_cols]))
OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[low_cardinality_cols]))
OH_cols_train.index = X_train.index
OH_cols_valid.index = X_valid.index
num_X_train = X_train.drop(object_cols, axis=1)
num_X_valid = X_valid.drop(object_cols, axis=1)
OH_X_train = pd.concat([num_X_train, OH_cols_train], axis=1)
OH_X_valid = pd.concat([num_X_valid, OH_cols_valid], axis=1)
OH_X_train.columns = OH_X_train.columns.astype(str)
OH_X_valid.columns = OH_X_valid.columns.astype(str)
```
