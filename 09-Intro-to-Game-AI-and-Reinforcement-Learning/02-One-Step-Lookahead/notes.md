# One-Step Lookahead

*Intro to Game AI and Reinforcement Learning — lesson 2* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/one-step-lookahead) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-one-step-lookahead)

## Key ideas

- A heuristic scores board positions; one-step lookahead picks the move with the best score.
- Weights for 2-, 3- and 4-in-a-row patterns shape the agent's behaviour.

## Functions and tools used

`drop_piece`, `get_heuristic`, `.copy`, `count_windows`, `.count`, `check_window`, `.reshape`, `.choice`, `np.asarray`, `.keys`, `evaluate`, `np.round`

## Exercise

### `q_1` — 1) A more complex heuristic

**My answer:**

```python
A = 1e10
B = 1e4
C = 1e2
D = -1
E = -1e6
```

### `q_2` — 2) Does the agent win?

**Discussion:** The agent has two choices: it can play in either column 0 (the leftmost column), or column 6 (the rightmost column). If the agent plays in column 0, it definitely wins the game in its next move.  And, if it plays in column 6, it likely loses the game (since, if the opponent responds by playing in the same column, then the opponent wins the game). 

If the agent uses the heuristic **from the tutorial**, both columns are scored equally, and so the agent will select from them (uniformly) at random.  In this case, the agent has about a 50/50 chance of winning the game. 

As for the heuristic **that** **you just implemented**, this will depend on your implementation, so we'll provide an answer for the solution heuristic that we provided -- in this case, the agent most likely loses the game, since it will definitely select the final column. 

This is an interesting situation, because on average, we see that the agent with the new heuristic performs better than the agent from the tutorial (and yet, for this board, it's guaranteed to make the wrong decision).

### `q_3` — 3) Submit to the competition

**Answer:**

```python
Follow the instructions to create an agent.
```
