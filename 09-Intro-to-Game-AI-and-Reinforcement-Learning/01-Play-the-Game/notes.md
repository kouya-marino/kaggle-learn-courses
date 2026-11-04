# Play the Game

*Intro to Game AI and Reinforcement Learning — lesson 1* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/play-the-game) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-play-the-game)

## Key ideas

- ConnectX environment; an agent is a function `agent(obs, config)` that returns a column.
- Simple rules (win if possible, otherwise block) already beat a random agent.

## Functions and tools used

`make`, `.run`, `.render`, `.choice`, `evaluate`, `np.round`, `.count`, `get_win_percentages`

## Exercise

### `q_1` — 1) A smarter agent

**My answer:**

```python
import random, inspect, os
def agent_q1(obs, config):
    valid_moves = [col for col in range(config.columns) if obs.board[col] == 0]
    for col in valid_moves:
        if check_winning_move(obs, config, col, obs.mark):
            return col
    return random.choice(valid_moves)
```

### `q_2` — 2) An even smarter agent

**My answer:**

```python
def agent_q2(obs, config):
    valid_moves = [col for col in range(config.columns) if obs.board[col] == 0]
    for col in valid_moves:
        if check_winning_move(obs, config, col, obs.mark):
            return col
    for col in valid_moves:
        if check_winning_move(obs, config, col, obs.mark % 2 + 1):
            return col
    return random.choice(valid_moves)
```

### `q_3` — 3) Looking ahead

**Discussion:** The agent can still lose the game, if 
- the opponent has set up the board so that it can win in the next move by dropping a disc in any of 2 or more columns, or 
- the only move that is available to the agent is one where, once played, the opponent can win in the next move.

### `q_4` — 4) Create your own agent

**Answer:**

```python
Follow the instructions to create an agent.
```

### `q_5` — 5) Submit to the competition

**My answer:**

```python
def write_agent_to_file(function, file):
    with open(file, "a" if os.path.exists(file) else "w") as f:
        f.write(inspect.getsource(function))
        print(function, "written to", file)
write_agent_to_file(my_agent, "submission.py")
```
