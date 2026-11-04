# Target Encoding

*Feature Engineering — lesson 6* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/target-encoding) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-target-encoding)

## Key ideas

- Target encoding replaces a category with a (smoothed) mean of the target.
- Fit the encoder on a separate split to avoid leakage; `MEstimateEncoder` with smoothing `m`.

## Functions and tools used

`pd.read_csv`, `.transform`, `.head`, `.groupby`, `.use`, `plt.rc`, `.filterwarnings`, `.astype`, `.format`, `.nunique`, `.copy`, `.pop`

## Exercise

### `q_1` — 1) Choose Features for Encoding

**Discussion:** The `Neighborhood` feature looks promising. It has the most categories of any feature, and several categories are rare. Others that could be worth considering are `SaleType`, `MSSubClass`, `Exterior1st`, `Exterior2nd`. In fact, almost any of the nominal features would be worth trying because of the prevalence of rare categories.

### `q_2` — 2) Apply M-Estimate Encoding

**My answer:**

```python
encoder = MEstimateEncoder(cols=["Neighborhood"], m=1.0)
encoder.fit(X_encode, y_encode)
X_train = encoder.transform(X_pretrain, y_train)
```

### `q_3` — 3) Overfitting with Target Encoders

**Discussion:** Since `Count` never has any duplicate values, the mean-encoded `Count` is essentially an exact copy of the target. In other words, mean-encoding turned a completely meaningless feature into a perfect feature.

Now, the only reason this worked is because we trained XGBoost on the same set we used to train the encoder. If we had used a hold-out set instead, none of this "fake" encoding would have transferred to the training data.

The lesson is that when using a target encoder it's very important to use separate data sets for training the encoder and training the model. Otherwise the results can be very disappointing!
