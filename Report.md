
## Project Navigation - Report


### 1. Overview Of The Project
> The projects goal is to train an agent to collect yellow bananas and avoid blue bananas by navigating in a virtual environment. We use reinforcement learning technique called to DQN to train the agent in this case. The agent is rewarded when it collects the yellow ones and penalize for the blue ones. 

### 2.  About Reinforcement Learning

#### 2.1 What is Reinforcement Learning
> Reinforcement learning is an area of Machine Learning. It is about taking suitable action to maximize reward in a particular situation. It is employed by various software and machines to find the best possible behavior or path it should take in a specific situation. Reinforcement learning differs from the supervised learning in a way that in supervised learning the training data has the answer key with it so the model is trained with the correct answer itself whereas in reinforcement learning, there is no answer but the reinforcement agent decides what to do to perform the given task.

#### 2.2 Different Techniques in RL
> There are two different reinforcement techniques Monte Carlo, Temporal difference (TD) learning and Q learning

> Monte Carlo:
> Monte Carlo (MC) methods are a subset of computational algorithms that use the process of repeated random sampling to make numerical estimations of unknown parameters. They allow for the modeling of complex situations where many random variables are involved, and assessing the impact of risk. The uses of MC are incredibly wide-ranging, and have led to a number of groundbreaking discoveries in the fields of physics, game theory, and finance.

> Temporal difference (TD) learning:
> Temporal difference (TD) learning refers to a class of model-free reinforcement learning methods which learn by bootstrapping from the current estimate of the value function. These methods sample from the environment, like Monte Carlo methods, and perform updates based on current estimates, like dynamic programming methods.While Monte Carlo methods only adjust their estimates once the final outcome is known, TD methods adjust predictions to match later, more accurate, predictions about the future before the final outcome is known.

> Q learning:
> Q-learning is a model-free reinforcement learning algorithm to learn a policy telling an agent what action to take under what circumstances. It does not require a model (hence the connotation "model-free") of the environment, and it can handle problems with stochastic transitions and rewards, without requiring adaptations.

#### 2.3 What is Deep Q Learning

> In deep Q-learning, we use a neural network to approximate the Q-value function. The state is given as the input and the Q-value of all possible actions is generated as the output. The comparison between Q-learning & deep Q-learning is wonderfully illustrated below:
![image.png](attachment:image.png)



> > The loss function here is mean squared error of the predicted Q-value and the target Q-value – Q*. This is basically a regression problem. However, we do not know the target or actual value here as we are dealing with a reinforcement learning problem. Going back to the Q-value update equation derived fromthe Bellman equation. 
![image.png](attachment:image.png)

#### 2.4 Problem With Deep Reinforcement Learning
> The major problem with deep reinforcement learning is its  instability when the network is used to represent the action values. So we use two methods called Experience replay and fixed q targets to fix this.

> Experience Replay : Experience replay enables reinforcement learning agents to memorize and reuse past experiences, just as humans replay memories for the situation at hand. Contemporary off-policy algorithms either replay past experiences uniformly or utilize a rulebased replay strategy, which may be sub-optimal. In this work, we consider learning a replay policy to optimize the cumulative reward.

> Fixed Q Targets : We saw in the Deep Q Learning chaper that, when we want to calculate the TD error (aka the loss), we calculate the difference between the TD target (Q_target) and the current Q value (estimation of Q).

![image.png](attachment:image.png)


> But we don’t have any idea of the real TD target. We need to estimate it. Using the Bellman equation, we saw that the TD target is just the reward of taking that action at that state plus the discounted highest Q value for the next state.
![image.png](attachment:image.png)

> However, the problem is that we using the same parameters (weights) for estimating the target and the Q value. As a consequence, there is a big correlation between the TD target and the parameters (w) we are changing.Therefore, it means that at every step of training, our Q values shift but also the target value shifts. So, we’re getting closer to our target but the target is also moving. It’s like chasing a moving target! This lead to a big oscillation in training.

> Instead, we can use the idea of fixed Q-targets introduced by DeepMind. Using a separate network with a fixed parameter (let’s call it w-) for estimating the TD target. At every Tau step, we copy the parameters from our DQN network to update the target network.

> Instead, we can use the idea of fixed Q-targets introduced by DeepMind. Using a separate network with a fixed parameter (let’s call it w-) for estimating the TD target. At every Tau step, we copy the parameters from our DQN network to update the target network.
![image.png](attachment:image.png)

### 3. Result

> The agent solved the environment in 447 episodes with an average score of 13.02, which meet the project's expectation. 
![image.png](attachment:image.png)

### 4. Improvement That Can Be Made
> We can use Prioritized Replay, which showed a significant improvement over DQN's, which might work in this case too.
> Other improvements such as Noisy deep q network and Distributional deep q network can be added to the original deep q network.


```python

```
