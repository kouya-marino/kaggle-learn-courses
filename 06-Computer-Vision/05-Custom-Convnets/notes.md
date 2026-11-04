# Custom Convnets

*Computer Vision — lesson 5* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/custom-convnets) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-custom-convnets)

## Key ideas

- Build a convnet from scratch with blocks of `Conv2D` + `MaxPool2D`, increasing filters per block.
- Finish with `Flatten` and dense layers; compile with binary cross-entropy for two classes.

## Functions and tools used

`set_seed`, `plt.rc`, `.filterwarnings`, `image_dataset_from_directory`, `.prefetch`, `.seed`, `.cache`, `.map`, `layers.Conv2D`, `layers.MaxPool2D`, `layers.Dense`, `.plot`

## Exercise

### `q_1` — 1) Define Model #

**My answer:**

```python
from tensorflow import keras
from tensorflow.keras import layers
model = keras.Sequential([
    layers.Conv2D(filters=32, kernel_size=3, activation='relu', padding='same', input_shape=[128, 128, 3]),
    layers.MaxPool2D(),
    layers.Conv2D(filters=64, kernel_size=3, activation='relu', padding='same'),
    layers.MaxPool2D(),
    layers.Conv2D(filters=128, kernel_size=3, activation='relu', padding='same'),
    layers.Conv2D(filters=128, kernel_size=3, activation='relu', padding='same'),
    layers.MaxPool2D(),
    layers.Flatten(),
    layers.Dense(6, activation='relu'),
    layers.Dropout(0.2),
    layers.Dense(1, activation='sigmoid'),
])
```

### `q_2` — 2) Compile #

**Answer:**

```python
model.compile(
    optimizer=tf.keras.optimizers.Adam(learning_rate=0.0001),
    loss='binary_crossentropy',
    metrics=['binary_accuracy'],
)
```

### `q_3` — 3) Train the Model #

**Discussion:** The learning curves for the model from the tutorial diverged fairly rapidly. This would indicate that it was prone to overfitting and in need of some regularization. The additional layer in our new model would make it even more prone to overfitting. However, adding some regularization with the `Dropout` layer helped prevent this. These changes improved the validation accuracy of the model by several points.
