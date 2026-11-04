# Deep Reinforcement Learning

*Intro to Game AI and Reinforcement Learning — lesson 4* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/deep-reinforcement-learning) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-deep-reinforcement-learning)

## Key ideas

- Deep RL trains a neural-network policy from rewards instead of hand-written rules.
- Wrap the game as a gym environment and train with PPO; reward design matters.

## Functions and tools used

`make`, `.train`, `.Discrete`, `.reshape`, `np.array`, `.Sequential`, `.Conv2d`, `.ReLU`, `.cnn`, `evaluate`, `np.round`, `.count`

## Exercise

### `q_1` — 1) Set the architecture

**My answer:**

```python
best_option = 'C'
```

### `q_2` — 2) Decide reward

**Discussion:** Here's a possible solution - after each move, we give the agent a reward that tells it how well it did:
- If agent wins the game in that move, it gets a reward of `+1`.
- Else if the agent selects an invalid move, it gets a reward of `-10`.
- Else if it detonates a mine, it gets a reward of `-1`.
- Else if the agent clears a square with no hidden mine, it gets a reward of `+1/100`.

To check the validity of your answer, note that the reward for selecting an invalid move and for detonating a mine should both be negative.  The reward for winning the game should be positive.  And, the reward for clearing a square with no hidden mine should be either zero or slightly positive.
