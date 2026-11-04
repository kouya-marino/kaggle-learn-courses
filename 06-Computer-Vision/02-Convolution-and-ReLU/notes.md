# Convolution and ReLU

*Computer Vision — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/convolution-and-relu) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-convolution-and-relu)

## Key ideas

- Convolution applies a kernel to detect features; ReLU keeps the positive responses.
- `tf.nn.conv2d` and `tf.nn.relu` show the filter → detect steps on a real image.

## Functions and tools used

`np.array`, `plt.get_cmap`, `plt.imshow`, `plt.xticks`, `cmap`, `keras.Sequential`, `layers.Conv2D`, `plt.rc`, `plt.figure`, `plt.axis`, `plt.show`, `tf.squeeze`

## Exercise

### `q_1` — 1) Define Kernel #

**My answer:**

```python
kernel = tf.constant([
    [-2, -1, 0],
    [-1, 1, 1],
    [0, 1, 2],
])
```

### `q_2` — 2) Apply Convolution #

**My answer:**

```python
conv_fn = tf.nn.conv2d
```

### `q_3` — 3) Apply ReLU #

**My answer:**

```python
relu_fn = tf.nn.relu
```

### `q_4` — 4) Observe Convolution on a Numerical Matrix #

**Discussion:** In the tutorial, we talked about how the pattern of positive numbers will tell you the kind of features the kernel will extract. This kernel has a vertical column of 1's, and so we would expect it to return features of vertical lines.
