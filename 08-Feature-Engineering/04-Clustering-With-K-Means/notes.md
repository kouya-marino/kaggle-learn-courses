# Clustering With K-Means

*Feature Engineering — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/clustering-with-k-means) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-clustering-with-k-means)

## Key ideas

- k-means cluster labels can be added as a categorical feature.
- Scaling choices matter; distances to each centroid make extra features.

## Functions and tools used

`.use`, `plt.rc`, `pd.read_csv`, `.head`, `KMeans`, `.fit_predict`, `.astype`, `sns.relplot`, `sns.catplot`

## Exercise

### `q_1` — 1) Scaling Features

**Discussion:** 1. No, since rescaling would distort the natural distances described by Latitude and Longitude.
2. Either choice could be reasonable, but because the living area of a home tends to be more valuable per square foot, it would make sense to rescale these features so that lot area isn't weighted in the clustering out of proportion to its effect on `SalePrice`, if that is what you were trying to predict.
3. Yes, since these don't have comparable units. Without rescaling, the number of doors in a car (usually 2 or 4) would have negligible weight compared to its horsepower (usually in the hundreds).

What you should take away from this is that the decision of whether and how to rescale features is rarely automatic -- it will usually depend on some domain knowledge about your data and what you're trying to predict. Comparing different rescaling schemes through cross-validation can also be helpful. (You might like to check out the `preprocessing` module in scikit-learn for some of the rescaling methods it offers.)

### `q_2` — 2) Create a Feature of Cluster Labels

**My answer:**

```python
X = df.copy()
y = X.pop("SalePrice")
features = ["LotArea", "TotalBsmtSF", "FirstFlrSF", "SecondFlrSF", "GrLivArea"]
X_scaled = X.loc[:, features]
X_scaled = (X_scaled - X_scaled.mean(axis=0)) / X_scaled.std(axis=0)
kmeans = KMeans(n_clusters=10, n_init=10, random_state=0)
X["Cluster"] = kmeans.fit_predict(X_scaled)
```

### `q_3` — 3) Cluster-Distance Features

**My answer:**

```python
kmeans = KMeans(n_clusters=10, n_init=10, random_state=0)
X_cd = kmeans.fit_transform(X_scaled)
X_cd = pd.DataFrame(X_cd, columns=[f"Centroid_{i}" for i in range(X_cd.shape[1])])
X = X.join(X_cd)
```
