# Overfitting and Underfitting

*Intro to Deep Learning — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/overfitting-and-underfitting) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-overfitting-and-underfitting)

## Key ideas

- Learning curves show underfitting (both losses high) or overfitting (validation loss rises).
- Increase capacity with wider / deeper networks.
- `EarlyStopping(patience, min_delta, restore_best_weights)` stops training at the best point.

## Functions and tools used

`EarlyStopping`, `pd.read_csv`, `.sample`, `.drop`, `.head`, `.EarlyStopping`, `keras.Sequential`, `.compile`, `layers.Dense`, `.fit`, `pd.DataFrame`, `.plot`

## Exercise

### `q_1` — 1) Evaluate Baseline

**Discussion:** The gap between these curves is quite small and the validation loss never increases, so it's more likely that the network is underfitting than overfitting. It would be worth experimenting with more capacity to see if that's the case.

### `q_2` — 2) Add Capacity

**Discussion:** Now the validation loss begins to rise very early, while the training loss continues to decrease. This indicates that the network has begun to overfit. At this point, we would need to try something to prevent it, either by reducing the number of units or through a method like early stopping. (We'll see another in the next lesson!)

### `q_3` — 3) Define Early Stopping Callback

**My answer:**

```python
early_stopping = callbacks.EarlyStopping(patience=5, min_delta=0.001, restore_best_weights=True)
```

### `q_4` — 4) Train and Interpret

**Discussion:** The early stopping callback did stop the training once the network began overfitting. Moreover, by including `restore_best_weights` we still get to keep the model where validation loss was lowest.
