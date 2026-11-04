# Dropout and Batch Normalization

*Intro to Deep Learning — lesson 5* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/dropout-and-batch-normalization) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-dropout-and-batch-normalization)

## Key ideas

- `Dropout` randomly drops units during training to reduce overfitting.
- `BatchNormalization` rescales activations and stabilises / speeds up training.

## Functions and tools used

`.use`, `plt.rc`, `pd.read_csv`, `.sample`, `.drop`, `keras.Sequential`, `layers.Dense`, `layers.Dropout`, `layers.BatchNormalization`, `.compile`, `.fit`, `pd.DataFrame`

## Exercise

### `q_1` — 1) Add Dropout to Spotify Model

**My answer:**

```python
model = keras.Sequential([
    layers.Dense(128, activation='relu', input_shape=input_shape),
    layers.Dropout(0.3),
    layers.Dense(64, activation='relu'),
    layers.Dropout(0.3),
    layers.Dense(1),
])
```

### `q_2` — 2) Evaluate Dropout

**Discussion:** From the learning curves, you can see that the validation loss remains near a constant minimum even though the training loss continues to decrease. So we can see that adding dropout did prevent overfitting this time. Moreover, by making it harder for the network to fit spurious patterns, dropout may have encouraged the network to seek out more of the true patterns, possibly improving the validation loss some as well).

### `q_3` — 3) Add Batch Normalization Layers

**My answer:**

```python
model = keras.Sequential([
    layers.BatchNormalization(input_shape=input_shape),
    layers.Dense(512, activation='relu'),
    layers.BatchNormalization(),
    layers.Dense(512, activation='relu'),
    layers.BatchNormalization(),
    layers.Dense(512, activation='relu'),
    layers.BatchNormalization(),
    layers.Dense(1),
])
```

### `q_4` — 4) Evaluate Batch Normalization

**Discussion:** You can see that adding batch normalization was a big improvement on the first attempt! By adaptively scaling the data as it passes through the network, batch normalization can let you train models on difficult datasets.
