# Deep Neural Networks

*Intro to Deep Learning — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/deep-neural-networks) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-deep-neural-networks)

## Key ideas

- Stacking `Dense` layers with non-linear activations (ReLU) lets a network learn complex relationships.
- Activations can also be added as separate `layers.Activation` layers.

## Functions and tools used

`keras.Sequential`, `layers.Dense`

## Exercise

### `q_1` — 1) Input Shape #

**My answer:**

```python
from tensorflow import keras
from tensorflow.keras import layers
input_shape = [8]
```

### `q_2` — 2) Define a Model with Hidden Layers #

**My answer:**

```python
model = keras.Sequential([
    layers.Dense(512, activation='relu', input_shape=input_shape),
    layers.Dense(512, activation='relu'),
    layers.Dense(512, activation='relu'),
    layers.Dense(1),
])
```

### `q_3` — 3) Activation Layers #

**My answer:**

```python
model = keras.Sequential([
    layers.Dense(32, input_shape=[8]),
    layers.Activation('relu'),
    layers.Dense(32),
    layers.Activation('relu'),
    layers.Dense(1),
])
```
