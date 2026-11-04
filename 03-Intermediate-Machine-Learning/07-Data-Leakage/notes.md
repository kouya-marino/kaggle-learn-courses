# Data Leakage

*Intermediate Machine Learning — lesson 7* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/data-leakage) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-data-leakage)

## Key ideas

- Target leakage: features that are only known after the outcome.
- Train-test contamination: preprocessing that sees validation data.
- Suspiciously high accuracy is a warning sign; keep preprocessing inside the pipeline / CV.

## Functions and tools used

`pd.read_csv`, `.drop`, `.head`, `make_pipeline`, `cross_val_score`, `RandomForestClassifier`, `.mean`

## Exercise

### `q_1` — Step 1: The Data Science of Shoelaces

**Discussion:** This is tricky, and it depends on details of how data is collected (which is common when thinking about leakage). Would you at the beginning of the month decide how much leather will be used that month? If so, this is ok. But if that is determined during the month, you would not have access to it when you make the prediction. If you have a guess at the beginning of the month, and it is subsequently changed during the month, the actual amount used during the month cannot be used as a feature (because it causes leakage).

### `q_2` — Step 2: Return of the Shoelaces

**Discussion:** This could be fine, but it depends on whether they order shoelaces first or leather first. If they order shoelaces first, you won't know how much leather they've ordered when you predict their shoelace needs. If they order leather first, then you'll have that number available when you place your shoelace order, and you should be ok.

### `q_3` — Step 3: Getting Rich With Cryptocurrencies?

**Discussion:** There is no source of leakage here. These features should be available at the moment you want to make a predition, and they're unlikely to be changed in the training data after the prediction target is determined. But, the way he describes accuracy could be misleading if you aren't careful. If the price moves gradually, today's price will be an accurate predictor of tomorrow's price, but it may not tell you whether it's a good time to invest. For instance, if it is $100 today, a model predicting a price of $100 tomorrow may seem accurate, even if it can't tell you whether the price is going up or down from the current price. A better prediction target would be the change in price over the next day. If you can consistently predict whether the price is about to go up or down (and by how much), you may have a winning investment opportunity.

### `q_4` — Step 4: Preventing Infections

**Discussion:** This poses a risk of both target leakage and train-test contamination (though you may be able to avoid both if you are careful).

You have target leakage if a given patient's outcome contributes to the infection rate for his surgeon, which is then plugged back into the prediction model for whether that patient becomes infected. You can avoid target leakage if you calculate the surgeon's infection rate by using only the surgeries before the patient we are predicting for. Calculating this for each surgery in your training data may be a little tricky.

You also have a train-test contamination problem if you calculate this using all surgeries a surgeon performed, including those from the test-set. The result would be that your model could look very accurate on the test set, even if it wouldn't generalize well to new patients after the model is deployed. This would happen because the surgeon-risk feature accounts for data in the test set. Test sets exist to estimate how the model will do when seeing new data. So this contamination defeats the purpose of the test set.

### `q_5` — Step 5: Housing Prices

**My answer:**

```python
potential_leakage_feature = 2
```
