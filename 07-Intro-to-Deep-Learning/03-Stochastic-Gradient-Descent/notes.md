# Stochastic Gradient Descent

*Intro to Deep Learning — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/stochastic-gradient-descent) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-stochastic-gradient-descent)

## Key ideas

- Training needs a loss (MAE / MSE) and an optimizer (Adam).
- SGD updates weights on minibatches; one pass over the data is an epoch.
- `model.compile(...)` then `model.fit(...)`; the returned `history` holds the learning curves.

## Functions and tools used

`pd.read_csv`, `.sample`, `.drop`, `.head`, `keras.Sequential`, `layers.Dense`, `.compile`, `.fit`, `pd.DataFrame`, `.plot`

## Exercise

### `q_1` — 1) Add Loss and Optimizer

**My answer:**

```python
model.compile(optimizer='adam', loss='mae')
```

### `q_2` — 2) Train Model

**My answer:**

```python
history = model.fit(X, y, batch_size=128, epochs=200, verbose=0)
```

### `q_3` — 3) Evaluate Training

**Discussion:** This depends on how the loss has evolved during training: if the learning curves have levelled off, there won't usually be any advantage to training for additional epochs.  Conversely, if the loss appears to still be decreasing, then training for longer could be advantageous.

### `q_4` — 4) Learning Rate and Batch Size

**Discussion:** You probably saw that smaller batch sizes gave noisier weight updates and loss curves. This is because each batch is a small *sample* of data and smaller samples tend to give noisier estimates. Smaller batches can have an "averaging" effect though which can be beneficial.

Smaller learning rates make the updates smaller and the training takes longer to converge. Large learning rates can speed up training, but don't "settle in" to a minimum as well. When the learning rate is too large, the training can fail completely. (Try setting the learning rate to a large value like 0.99 to see this.)
