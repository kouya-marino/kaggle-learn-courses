# Maximum Pooling

*Computer Vision — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/maximum-pooling) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-maximum-pooling)

## Key ideas

- Max pooling condenses feature maps and gives some translation invariance.
- Global average pooling reduces each feature map to one number before the head.

## Functions and tools used

`keras.Sequential`, `layers.Conv2D`, `layers.MaxPool2D`, `plt.rc`, `.filterwarnings`, `plt.figure`, `plt.subplot`, `plt.imshow`, `plt.axis`, `plt.title`, `plt.show`, `tf.squeeze`

## Exercise

### `q_1` — 1) Apply Pooling to Condense #

**My answer:**

```python
image_condense = tf.nn.pool(input=image_detect, window_shape=(2, 2), pooling_type='MAX', strides=(2, 2), padding='SAME')
```

### `q_2` — 2) Explore Invariance #

**Discussion:** In the tutorial, we talked about how maximum pooling creates **translation invariance** over small distances. This means that we would expect small shifts to disappear after repeated maximum pooling. If you run the cell multiple times, you can see the resulting image is always the same; the pooling operation destroys those small translations.

### `q_3` — 3) Understand the Pooled Features #

**Discussion:** The VGG16 base produces 512 feature maps. We can think of each feature map as representing some high-level visual feature in the original image -- maybe a wheel or window. Pooling a map gives us a single number, which we could think of as a *score* for that feature: large if the feature is present, small if it is absent. Cars tend to score high with one set of features, and Trucks score high with another. Now, instead of trying to map raw features to classes, the head only has to work with these scores that `GlobalAvgPool2D` produced, a much easier problem for it to solve.
