# The Sliding Window

*Computer Vision — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/ryanholbrook/the-sliding-window) · [Exercise on Kaggle](https://www.kaggle.com/code/ryanholbrook/exercise-the-sliding-window)

## Key ideas

- Stride and padding (`valid` vs `same`) control how the window moves and the output size.
- The same sliding-window idea works on 1D signals such as time series.

## Functions and tools used

`np.zeros`, `.circle_perimeter`, `.resize`, `np.array`, `plt.get_cmap`, `plt.imshow`, `plt.xticks`, `tf.reshape`, `.update`, `cmap`, `plt.rc`, `show_extraction`

## Exercise

### `q_1` — 1) Growing the Receptive Field #

**Discussion:** The third layer would have a $7 \times 7$ receptive field.
