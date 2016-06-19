Tutorial 5: Deep Q-learning
========

Up until this tutorial Q-learning algorithm has been storing state-action pairs in a table, a dictionary or a similar kind of data structure. The fact is that there're many scenarios where tables don't scale nicely. Let's take Pacman. If we implement it as a graphics-based game, the state would be the raw pixel data. In a tabular method, if the pixel data changes by just a single pixel, we have to store that as a completely separate entry in the table. Obviously that's silly and wasteful. What we need is **some way to generalize and pattern match between states**. We need our algorithm to say "the value of these kind of states is X" rather than "the value of this exact, super specific state is X."

That's where neural networks come in. Or any other type of function approximator, even a simple linear model. We can use a neural network, instead of a lookup table, as our  Q(s,a)Q(s,a)  function. Just like before, it will accept a state and an action and spit out the value of that state-action.

### A bit of theoretical background
Discuss Deepmind's papers and original DQN algorithm.

(from second paper)
>Reinforcement learning is known to be unstable or even to diverge when a nonlinear function approximator such as a neural network is used to represent the action-value (also known as Q) function20.

### Playing with the hyperparameters in a DQN:

#### Network architecture
#### Minibatch size
#### Memory size
#### Learning rate

#### Changing the rewards
Changing the rewards proved to be relevant when working with Q-learning however it seems that with DQN, it's not that much. In fact the [0, 1] rewards outperformed the [-200,0,200] artificial rewards under the same hyperparameters:

| Algorithm | `epochs:` 100 | `epochs:` 500  | `epochs:` 1000  |
|-----------|----------------|----------------|-----------------|
| DQN (default params) [4x30x30x2`]	| 24 (17) | 200 (199) | 200 (168)|
| DQN (default params), default rewards [4x30x30x2`]	| 9 (15) | 200 (199) | 200 (199) |



### Comparing different techniques in `CartPole`


| Algorithm | `epochs:` 100 | `epochs:` 500  | `epochs:` 1000  |
|-----------|----------------|----------------|-----------------|
| Q-learning| 104.87 (86.37) | 181.22 (145.78) | 191.35 (141.31) |
| DQN (default params) [4x30x30x2`]	| 24 (17) | 200 (199) | 200 (168)|
| DQN (default params) [4x30x30x30x2`]	| 71 (26) | 150 (184) | 120 (126) |
| DQN (default params), default rewards [4x30x30x2`]	| 9 (15) | 200 (199) | 200 (199) |

*Each cell represents the best 100 scores for the number of epochs and in parenthesis the average score over all the epochs*

For the DQN, the default parameters (default params) correspond with:
```
epochs = 1000
steps = 100000
updateTargetNetwork = 10000
explorationRate = 1
minibatch_size = 128
learnStart = 128
learningRate = 0.00025
discountFactor = 0.99
memorySize = 1000000

```

### References:
- http://deeplearning.net/tutorial/mlp.html#mlp
- http://outlace.com/Reinforcement-Learning-Part-3/
- https://gist.github.com/wingedsheep/4199594b02138dd427c22a540d6d6b8d#file-cartpole_runnner-py-L54
- http://keras.io/
- http://ufldl.stanford.edu/tutorial/supervised/MultiLayerNeuralNetworks/
- https://github.com/sherjilozair/dqn
- https://github.com/VinF/deer
