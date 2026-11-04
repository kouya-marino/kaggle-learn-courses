# Basic Data Exploration

*Intro to Machine Learning — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/dansbecker/basic-data-exploration) · [Exercise on Kaggle](https://www.kaggle.com/code/dansbecker/exercise-explore-your-data)

## Key ideas

- Load data with pandas and read `describe()` (count, mean, std, min/max, quartiles) before modelling.
- Understanding the columns comes before choosing features.

## Functions and tools used

`pd.read_csv`, `.describe`

## Exercise

### `step_1` — Step 1: Loading Data

**My answer:**

```python
import datetime
import pandas as pd
iowa_file_path = '../input/home-data-for-ml-course/train.csv'
home_data = pd.read_csv(iowa_file_path)
```

### `step_2` — Step 2: Review The Data

**My answer:**

```python
print(home_data.describe())
avg_lot_size = round(home_data.LotArea.mean())
newest_home_age = datetime.datetime.now().year - home_data.YearBuilt.max()
```
