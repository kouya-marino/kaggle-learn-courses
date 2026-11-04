# N-Step Lookahead

*Intro to Game AI and Reinforcement Learning — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/n-step-lookahead) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-n-step-lookahead)

## Key ideas

- Minimax searches N moves ahead, assuming the opponent plays its best reply.
- The game tree grows quickly (7 moves per level), so depth is limited.

## Functions and tools used

`.copy`, `.count`, `check_window`, `count_windows`, `drop_piece`, `minimax`, `is_terminal_node`, `get_heuristic`, `is_terminal_window`, `.reshape`, `evaluate`, `np.round`

## Exercise

### `q_1` — 1) A closer look

**Discussion:** The first heuristic is guaranteed to select column 2 to block the opponent from winning.  The second heuristic selects either column 2 or column 3 (where it selects each with 50% probability). Thus, for this game board, the first heuristic is better. In general, we can expect that the first heuristic is a better heuristic, since we cannot trust the second heuristic to block the opponent from winning.

### `q_2` — 2) Count the leaves

**My answer:**

```python
num_leaves = 7*7*7
```

### `q_3` — 3) Which move will the agent select?

**My answer:**

```python
selected_move = 3
```

### `q_4` — 4) Examine the assumptions

**Discussion:** We can still expect the minimax agent to perform well. On a high level, assuming an optimal opponent simply overestimates the opponent, but does not break the algorithm.  The effect of overestimating the opponent is merely that the minimax agent will take longer to win, than if it had a more accurate understanding of its opponent.  For instance, the minimax agent is highly unlikely to select the same column three times in its first three moves (since it assumes an optimal opponent that will certainly block the winning play in the next move), but this is not a bad initial strategy for playing against an agent that selects columns completely at random.

### `q_5` — 5) Submit to the competition

**Answer:**

```python
Follow the instructions to create an agent.
```
