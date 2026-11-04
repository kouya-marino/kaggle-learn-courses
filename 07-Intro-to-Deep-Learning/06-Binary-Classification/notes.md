# Binary Classification

*Intro to Deep Learning — lesson 6* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/binary-classification) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-binary-classification)

## Key ideas

- Binary classification uses a sigmoid output and binary cross-entropy loss.
- Track accuracy (`binary_accuracy`) alongside the loss.

## Functions and tools used

`pd.read_csv`, `.copy`, `.map`, `.sample`, `.drop`, `.dropna`, `.head`, `keras.Sequential`, `layers.Dense`, `.compile`, `.EarlyStopping`, `.plot`

## Exercise

### `q_1` — 1) Define Model #

**My answer:**

```python
from tensorflow import keras
from tensorflow.keras import layers
model = keras.Sequential([
    layers.BatchNormalization(input_shape=input_shape),
    layers.Dense(256, activation='relu'),
    layers.BatchNormalization(),
    layers.Dropout(0.3),
    layers.Dense(256, activation='relu'),
    layers.BatchNormalization(),
    layers.Dropout(0.3),
    layers.Dense(1, activation='sigmoid'),
])
```

### `q_2` — 2) Add Optimizer, Loss, and Metric #

**My answer:**

```python
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['binary_accuracy'])
```

### `q_3` — 3) Train and Evaluate #

**Discussion:** Though we can see the training loss continuing to fall, the early stopping callback prevented any overfitting. Moreover, the accuracy rose at the same rate as the cross-entropy fell, so it appears that minimizing cross-entropy was a good stand-in. All in all, it looks like this training was a success!
