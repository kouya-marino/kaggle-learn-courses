# Exercise (solved): Deep Reinforcement Learning


**This notebook is an exercise in the [Intro to Game AI and Reinforcement Learning](https://www.kaggle.com/learn/intro-to-game-ai-and-reinforcement-learning) course.  You can reference the tutorial at [this link](https://www.kaggle.com/alexisbcook/deep-reinforcement-learning).**

---

# Introduction

In the tutorial, you learned a bit about reinforcement learning and used the `stable-baselines3` package to train an agent to beat a random opponent.  In this exercise, you will check your understanding and tinker with the code to deepen your intuition.

```python
from learntools.core import binder
binder.bind(globals())
from learntools.game_ai.ex4 import *
```

### 1) Set the architecture

In the tutorial, you learned one way to design a neural network that can select moves in Connect Four.  The neural network had an output layer with seven nodes: one for each column in the game board.

Say now you wanted to create a neural network that can play chess.  How many nodes should you put in the output layer?

- Option A: 2 nodes (number of game players)
- Option B: 16 nodes (number of game pieces that each player starts with)
- Option C: 4672 nodes (number of possible moves)
- Option D: 64 nodes (number of squares on the game board)

Use your answer to set the value of the `best_option` variable below.  Your answer should be one of `'A'`, `'B'`, `'C'`, or `'D'`.

```python
best_option = 'C'
q_1.check()
```

```python
# Lines below will give you solution code
#q_1.solution()
```

### 2) Decide reward

In the tutorial, you learned how to give your agent a reward that encourages it to win games of Connect Four.  Consider now training an agent to win at the game [Minesweeper](https://bit.ly/2T5xEY8).  The goal of the game is to clear the board without detonating any bombs.

To play this game in Google Search, click on the **[Play]** button at [this link](https://www.google.com/search?q=minesweeper).  

<center>
<img src="https://storage.googleapis.com/kaggle-media/learn/images/WzoEfKY.png" width=50%><br/>
</center>

With each move, one of the following is true:
- The agent selected an invalid move (in other words, it tried to uncover a square that was uncovered as part of a previous move).  Let's assume this ends the game, and the agent loses.
- The agent clears a square that did not contain a hidden mine.  The agent wins the game, because all squares without mines are revealed.
- The agent clears a square that did not contain a hidden mine, but has not yet won or lost the game.
- The agent detonates a mine and loses the game.

How might you specify the reward for each of these four cases, so that by maximizing the cumulative reward, the agent will try to win the game?

After you have decided on your answer, run the code cell below to get credit for completing this question.

```python
# Check your answer (Run this code cell to receive credit!)
q_2.solution()
```

### 3) (Optional) Amend the code

In this next part of the exercise, you will amend the code from the tutorial to experiment with creating your own agents!  There are a lot of hyperparameters involved with specifying a reinforcement learning agent, and you'll have a chance to amend them, to see how performance is affected.

First, we'll need to make sure that your Kaggle Notebook is set up to run the code.  Begin by looking at the "Settings" menu to the right of your notebook.  Your menu will look like one of the following:

<center>
<img src="https://storage.googleapis.com/kaggle-media/learn/images/kR1az0y.png" width=100%><br/>
</center>

If your "Internet" setting appears as a "Requires phone verification" link, click on this link.  This will bring you to a new window; then, follow the instructions to verify your account.  After following this step, your "Internet" setting will appear "Off", as in the example to the right.

Once your "Internet" setting appears as "Off", click to turn it on.  You'll see a pop-up window that you'll need to "Accept" in order to complete the process and have the setting switched to "On".  Once the Internet is turned "On", you're ready to proceed!

<center>
<img src="https://storage.googleapis.com/kaggle-media/learn/images/gOVh6Aa.png" width=100%><br/>
</center>

Begin by running the code cell below.

```python
import random
import numpy as np
import pandas as pd
import gym
import matplotlib.pyplot as plt
%matplotlib inline

from kaggle_environments import make, evaluate
from gym import spaces

class ConnectFourGym(gym.Env):
    def __init__(self, agent2="random"):
        ks_env = make("connectx", debug=True)
        self.env = ks_env.train([None, agent2])
        self.rows = ks_env.configuration.rows
        self.columns = ks_env.configuration.columns
        # Learn about spaces here: http://gym.openai.com/docs/#spaces
        self.action_space = spaces.Discrete(self.columns)
        self.observation_space = spaces.Box(low=0, high=2, 
                                            shape=(1,self.rows,self.columns), dtype=int)
        # Tuple corresponding to the min and max possible rewards
        self.reward_range = (-10, 1)
        # StableBaselines throws error if these are not defined
        self.spec = None
        self.metadata = None
    def reset(self):
        self.obs = self.env.reset()
        return np.array(self.obs['board']).reshape(1,self.rows,self.columns)
    def change_reward(self, old_reward, done):
        if old_reward == 1: # The agent won the game
            return 1
        elif done: # The opponent won the game
            return -1
        else: # Reward 1/42
            return 1/(self.rows*self.columns)
    def step(self, action):
        # Check if agent's move is valid
        is_valid = (self.obs['board'][int(action)] == 0)
        if is_valid: # Play the move
            self.obs, old_reward, done, _ = self.env.step(int(action))
            reward = self.change_reward(old_reward, done)
        else: # End the game and penalize agent
            reward, done, _ = -10, True, {}
        return np.array(self.obs['board']).reshape(1,self.rows,self.columns), reward, done, _
    
# Create ConnectFour environment 
env = ConnectFourGym(agent2="random")

import torch as th
import torch.nn as nn

!pip install "stable-baselines3"
from stable_baselines3 import PPO 
from stable_baselines3.common.torch_layers import BaseFeaturesExtractor

# Neural network for predicting action values
class CustomCNN(BaseFeaturesExtractor):
    
    def __init__(self, observation_space: gym.spaces.Box, features_dim: int=128):
        super(CustomCNN, self).__init__(observation_space, features_dim)
        # CxHxW images (channels first)
        n_input_channels = observation_space.shape[0]
        self.cnn = nn.Sequential(
            nn.Conv2d(n_input_channels, 32, kernel_size=3, stride=1, padding=0),
            nn.ReLU(),
            nn.Conv2d(32, 64, kernel_size=3, stride=1, padding=0),
            nn.ReLU(),
            nn.Flatten(),
        )

        # Compute shape by doing one forward pass
        with th.no_grad():
            n_flatten = self.cnn(
                th.as_tensor(observation_space.sample()[None]).float()
            ).shape[1]

        self.linear = nn.Sequential(nn.Linear(n_flatten, features_dim), nn.ReLU())

    def forward(self, observations: th.Tensor) -> th.Tensor:
        return self.linear(self.cnn(observations))

policy_kwargs = dict(
    features_extractor_class=CustomCNN,
)
```

Next, run the code cell below to train an agent with PPO.  This code is identical to the code from the tutorial.

```python
# Initialize agent
model = PPO("CnnPolicy", env, policy_kwargs=policy_kwargs, verbose=0)

# Train agent
model.learn(total_timesteps=50000)
```

Once you have verified that the code runs, try making amendments to see if you can get increased performance.  You might like to:
- learn more about the [`stable-baselines3` package](https://stable-baselines3.readthedocs.io/en/master/) to amend the agent.
- change `agent2` to a different agent when creating the ConnectFour environment with `env = ConnectFourGym(agent2="random")`.  For instance, you might like to use the `"negamax"` agent, or a different, custom agent.  Note that the smarter you make the opponent, the harder it will be for your agent to train!

# Congratulations!

You have completed the course, and it's time to put your new skills to work!  

The next step is to apply what you've learned to a **[more complex game: Halite](https://www.kaggle.com/c/halite)**.  For a step-by-step tutorial in how to make your first submission to this competition, **[check out the bonus lesson](https://www.kaggle.com/alexisbcook/getting-started-with-halite)**!

You can find more games as they're released on the **[Kaggle Simulations page](https://www.kaggle.com/simulations)**.

As we did in the course, we recommend that you start simple, with an agent that follows your precise instructions.  This will allow you to learn more about the mechanics of the game and to build intuition for what makes a good agent.  Then, gradually increase the complexity of your agents to climb the leaderboard!

---




*Have questions or comments? Visit the [course discussion forum](https://www.kaggle.com/learn/intro-to-game-ai-and-reinforcement-learning/discussion) to chat with other learners.*
