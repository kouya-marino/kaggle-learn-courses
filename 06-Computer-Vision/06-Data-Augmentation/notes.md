# Data Augmentation

*Computer Vision — lesson 6* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/data-augmentation) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-data-augmentation)

## Key ideas

- Data augmentation (random flip, contrast, rotation) creates more varied training images.
- Preprocessing layers inside the model plus batch normalization reduce overfitting.

## Functions and tools used

`set_seed`, `plt.rc`, `.filterwarnings`, `image_dataset_from_directory`, `.prefetch`, `.seed`, `.set_seed`, `.convert_image_dtype`, `.cache`, `.map`, `layers.Dense`, `.plot`

## Exercise

### `q_1` — 1) EuroSAT #

**Discussion:** It seems to this author that flips and rotations would be worth trying first since there's no concept of orientation for pictures taken straight overhead. None of the transformations seem likely to confuse classes, however.

### `q_2` — 2) TensorFlow Flowers #

**Discussion:** It seems to this author that horizontal flips and moderate rotations would be worth trying first. Some augmentation libraries include transformations of hue (like red to blue). Since the color of a flower seems distinctive of its class, a change of hue might be less successful. On the other hand, there is suprising variety in cultivated flowers like roses, so, depending on the dataset, this might be an improvement after all!

### `q_3` — 3) Add Preprocessing Layers #

**My answer:**

```python
model = keras.Sequential([
    layers.InputLayer(input_shape=[128, 128, 3]),
    preprocessing.RandomContrast(factor=0.10),
    preprocessing.RandomFlip(mode='horizontal'),
    preprocessing.RandomRotation(factor=0.10),
    layers.BatchNormalization(renorm=True),
    layers.Conv2D(filters=64, kernel_size=3, activation='relu', padding='same'),
    layers.MaxPool2D(),
    layers.BatchNormalization(renorm=True),
    layers.Conv2D(filters=128, kernel_size=3, activation='relu', padding='same'),
    layers.MaxPool2D(),
    layers.BatchNormalization(renorm=True),
    layers.Conv2D(filters=256, kernel_size=3, activation='relu', padding='same'),
    layers.Conv2D(filters=256, kernel_size=3, activation='relu', padding='same'),
    layers.MaxPool2D(),
    layers.BatchNormalization(renorm=True),
    layers.Flatten(),
    layers.Dense(8, activation='relu'),
    layers.Dense(1, activation='sigmoid'),
])
```

### `q_4` — 4) Train Model #

**Discussion:** The learning curves in this model stayed close together for much longer than in previous models. This suggests that the augmentation helped prevent overfitting, allowing the model to continue improving.

And notice that this model achieved the highest accuracy of all the models in the course! This won't always be the case, but it shows that a well-designed custom convnet can sometimes perform as well or better than a much larger pretrained model. Depending on your application, having a smaller model (which requires fewer resources) could be a big advantage.
