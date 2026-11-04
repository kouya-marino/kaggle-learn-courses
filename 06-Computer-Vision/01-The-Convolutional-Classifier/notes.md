# The Convolutional Classifier

*Computer Vision — lesson 1* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/the-convolutional-classifier) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-the-convolutional-classifier)

## Key ideas

- A convnet classifier = convolutional base (feature extraction) + dense head (classification).
- Transfer learning: reuse a pretrained base, freeze it (`trainable = False`) and train only the head.

## Functions and tools used

`set_seed`, `plt.rc`, `.filterwarnings`, `image_dataset_from_directory`, `.prefetch`, `.seed`, `.set_seed`, `.convert_image_dtype`, `.cache`, `.map`, `layers.Dense`, `.plot`

## Exercise

### `q_1` — 1) Define Pretrained Base #

**My answer:**

```python
from tensorflow import keras
from tensorflow.keras import layers
pretrained_base.trainable = False
```

### `q_2` — 2) Attach Head #

**My answer:**

```python
model = keras.Sequential([
    pretrained_base,
    layers.Flatten(),
    layers.Dense(6, activation='relu'),
    layers.Dense(1, activation='sigmoid'),
])
```

### `q_3` — 3) Train #

**My answer:**

```python
model.compile(optimizer=tf.keras.optimizers.Adam(epsilon=0.01), loss='binary_crossentropy', metrics=['binary_accuracy'])
```

### `q_4` — 4) Examine Loss and Accuracy #

**Discussion:** That the training loss and validation loss stay fairly close is evidence that the model isn't just memorizing the training data, but rather learning general properties of the two classes. But, because this model converges at a loss greater than the VGG16 model, it's likely that it is underfitting some, and could benefit from some extra capacity.
