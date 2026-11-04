# Principal Component Analysis

*Feature Engineering — lesson 5* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/principal-component-analysis) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-principal-component-analysis)

## Key ideas

- PCA finds directions of variation; loadings show what each component means.
- Standardise first; use components as features or as ideas for new features.

## Functions and tools used

`.use`, `plt.rc`, `pd.read_csv`, `plt.subplots`, `np.arange`, `.bar`, `np.cumsum`, `.plot`, `mutual_info_regression`, `pd.Series`, `.sort_values`, `pd.DataFrame`

## Exercise

### `q_1` — 1) Interpret Component Loadings

**Discussion:** The first component, `PC1`, seems to be a kind of "size" component, similar to what we saw in the tutorial: all of the features have the same sign (positive), indicating that this component is describing a contrast between houses having large values and houses having small values for these features.

The interpretation of the third component `PC3` is a little trickier. The features `GarageArea` and `YearRemodAdd` both have near-zero loadings, so let's ignore those. This component is mostly about `TotalBsmtSF` and `GrLivArea`. It describes a contrast between houses with a lot of living area but small (or non-existant) basements, and the opposite: small houses with large basements.

### `q_2` — 2) Create New Features

**My answer:**

```python
X["Feature1"] = X.GrLivArea + X.TotalBsmtSF
X["Feature2"] = X.YearRemodAdd * X.TotalBsmtSF
score = score_dataset(X, y)
print(f"Your score: {score:.5f} RMSLE")
```

### `q_3` — 3) Outlier Detection

**Discussion:** Notice that there are several dwellings listed as `Partial` sales in the `Edwards` neighborhood that stand out. A partial sale is what occurs when there are multiple owners of a property and one or more of them sell their "partial" ownership of the property.

These kinds of sales are often happen during the settlement of a family estate or the dissolution of a business and aren't advertised publicly. If you were trying to predict the value of a house on the open market, you would probably be justified in removing sales like these from your dataset -- they are truly outliers.
