# Creating Features

*Feature Engineering — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/creating-features) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-creating-features)

## Key ideas

- New features from maths (ratios, sums), counts, splitting / combining strings, and group transforms (`groupby().transform`).

## Functions and tools used

`.use`, `plt.rc`, `pd.read_csv`, `.head`, `.apply`, `plt.subplots`, `sns.kdeplot`, `.gt`, `.split`, `.transform`, `.groupby`, `.count`

## Exercise

### `q_1` — 1) Create Mathematical Transforms

**My answer:**

```python
X_1 = pd.DataFrame()
X_1["LivLotRatio"] = df.GrLivArea / df.LotArea
X_1["Spaciousness"] = (df.FirstFlrSF + df.SecondFlrSF) / df.TotRmsAbvGrd
X_1["TotalOutsideSF"] = df.WoodDeckSF + df.OpenPorchSF + df.EnclosedPorch + df.Threeseasonporch + df.ScreenPorch
```

### `q_2` — 2) Interaction with a Categorical

**My answer:**

```python
X_2 = pd.get_dummies(df.BldgType, prefix="Bldg")
X_2 = X_2.mul(df.GrLivArea, axis=0)
```

### `q_3` — 3) Count Feature

**My answer:**

```python
X_3 = pd.DataFrame()
X_3["PorchTypes"] = df[["WoodDeckSF", "OpenPorchSF", "EnclosedPorch", "Threeseasonporch", "ScreenPorch"]].gt(0.0).sum(axis=1)
```

### `q_4` — 4) Break Down a Categorical Feature

**My answer:**

```python
X_4 = pd.DataFrame()
X_4["MSClass"] = df.MSSubClass.str.split("_", n=1, expand=True)[0]
```

### `q_5` — 5) Use a Grouped Transform

**My answer:**

```python
X_5 = pd.DataFrame()
X_5["MedNhbdArea"] = df.groupby("Neighborhood")["GrLivArea"].transform("median")
```
