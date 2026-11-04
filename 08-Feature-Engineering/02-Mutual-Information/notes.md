# Mutual Information

*Feature Engineering — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/mutual-information) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-mutual-information)

## Key ideas

- Mutual information measures any kind of dependence between a feature and the target.
- Use MI scores to rank features; interaction plots show effects MI alone can't.

## Functions and tools used

`.use`, `pd.read_csv`, `.head`, `.copy`, `.pop`, `.select_dtypes`, `.factorize`, `make_mi_scores`, `mutual_info_regression`, `pd.Series`, `.sort_values`, `plt.figure`

## Exercise

### `q_1` — 1) Understand Mutual Information

**Discussion:** Based on the plots, `YearBuilt` should have the highest MI score since knowing the year tends to constrain `SalePrice` to a smaller range of possible values. This is generally not the case for `MoSold`, however. Finally, since `ScreenPorch` is usually just one value, 0, on average it won't tell you much about `SalePrice` (though more than `MoSold`) .

### `q_2` — 2) Examine MI Scores

**Discussion:** Some common themes among most of these features are:
- Location: `Neighborhood`
- Size: all of the `Area` and `SF` features, and counts like `FullBath` and `GarageCars`
- Quality: all of the `Qual` features
- Year: `YearBuilt` and `YearRemodAdd`
- Types: descriptions of features and styles like `Foundation` and `GarageType`

These are all the kinds of features you'll commonly see in real-estate listings (like on Zillow), It's good then that our mutual information metric scored them highly. On the other hand, the lowest ranked features seem to mostly represent things that are rare or exceptional in some way, and so wouldn't be relevant to the average home buyer.

### `q_3` — 3) Discover Interactions

**Discussion:** The trends lines within each category of `BldgType` are clearly very different, indicating an interaction between these features. Since knowing `BldgType` tells us more about how `GrLivArea` relates to `SalePrice`, we should consider including `BldgType` in our feature set.

The trend lines for `MoSold`, however, are almost all the same. This feature hasn't become more informative for knowing `BldgType`.
