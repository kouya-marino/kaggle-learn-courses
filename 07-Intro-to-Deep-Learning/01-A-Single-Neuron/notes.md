# A Single Neuron

*Intro to Deep Learning — lesson 1* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/a-single-neuron) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-a-single-neuron)

## Key ideas

- A linear unit computes `y = w·x + b`; in Keras that's `layers.Dense(units=1)`.
- `input_shape` is the number of features; weights start random.

## Functions and tools used

`keras.Sequential`, `layers.Dense`

## Exercise

### `q_1` — 1) Input shape #

**My answer:**

```python
from tensorflow import keras
from tensorflow.keras import layers
input_shape = [11]
```

### `q_2` — 2) Define a linear model

**My answer:**

```python
model = keras.Sequential([layers.Dense(units=1, input_shape=[11])])
```

### `q_3` — 3) Look at the weights

**Answer:** completed by running the provided code (see `exercise-solved.ipynb`).
