[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif 
"Trained Agent"

[image2]: 1.png  "1"
[image3]: 2.png  "2"
[image4]: 3.png  "3"
[image5]: 4.png  "4"
[image6]: 5.png  "5"

# Project 1: Navigation

### Introduction

For this project, we will train an agent to navigate (and collect bananas!) in a large, square world.  

![Trained Agent][image1]

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting 
a blue banana.  Thus, the goal of your agent is to collect as many yellow bananas as possible while 
avoiding blue bananas.  

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around agent's forward direction.  Given this information, the agent has to learn how to best select actions.  Four discrete actions are available, corresponding to:
- **`0`** - move forward.
- **`1`** - move backward.
- **`2`** - turn left.
- **`3`** - turn right.

### Completion criteria

The task is episodic, and in order to solve the environment, the agent must get an average score of +13 
over 100 consecutive episodes.

### Environment

The environment is simulated by Unity application _Banana_ lying in the subdirectory _Banana_Windows_x86_64_
We start the environment as follows:

_env = UnityEnvironment(file_name="Banana_Windows_x86_64/Banana.exe")_

### Training sessions

We run several training sessions in according  to the variable _numb_of_trains_.
For each training session, the obtained weights are saved into the file 'weights_'+str(train_numb)+'.trn'.
We get files: _weights_0.trn_,  _weights_1.trn_,  _weights_2.trn_,  etc.

For each training session, we construct the **agent** with different parameters
and we run the *Deep-Q-Network* procedure **dqn** as follows:

  agent = **Agent**(state_size=37, action_size=4, seed=1, fc1_units=fc1_nodes, fc2_units=fc2_nodes)       
  scores, episodes = **dqn**(n_episodes = 2000, eps_start = epsilon_start, train_numb=i)  
  
### Training parameters

We experience the following parameters:  _fc1_units_, _fc2_units_,  _eps_start_.
At the end of each session these parameters together with the episode number (at which the training is finished) 
are saved into the corresponding lists. These lists are used on the step of testing of weights.
For each training session, 
 * _eps_start_ is played out as a random value from 0.988 to 0.955 with step 0.001, 
 * _fc1_units_ is played out as a random value from 48 to 128 with step 16,
 * _fc2_inits_ is played out as a random value from fc1_units - 16 to fc1_units - 16 with step 8.

### Deep-Q-Network algorithm

The _Deep-Q-Network_ procedure **dqn** performs the **double loop**. 
External loop (by _episodes_) is executed till the number of episodes reached the maximal number 
of episodes _n_episodes = 2000_ or the _completion criteria_ is executed.
The environment _env_  is reset with the paarmeter _train_mode_=_True_.
For the completion criteria, we check  

  _np.mean(scores_window) >=13_,  

where _scores_window_ is the array of the type deque realizing  the shifting window of length <= 100.
The element _scores_window[i]_ contains the _score_ achieved by the algorithm on the episode _i_.


In the internal loop,  **dqn** gets the current _action_ from the **agent**.
By this _action_ **dqn** gets _state_ and _reward_ from Unity environment.
Then, the **agent** accept params _state,action,reward,next_state, done_
to the next training step. The variable _score_ accumulates obtained rewards.

### Agent

The class **Agent** is defined in _dqn_agent.py_. This is the well-known class implementing 
the following mechanisms:

* Two Q-Networks (local and target) using the simple neural network.
* Replay memory (using the class ReplayBuffer)
* Epsilon-greedy mechanism
* Q-learning, i.e., using the max value for all possible actions
* Computing the loss function by MSE loss
* Minimize the loss by gradient descend mechanism using the ADAM optimizer

### Model Q-Network

Both Q-Networks (local and target) are implemented by the class
**QNetwork** lying in the file _model.py_. This class implements the simple
neural network with 3 fully-connected layers and 2 
rectified nonlinear layers. This **QNetwork** is realized in the framework 
of package **PyTorch**. The number of neurons of the fully-connected layers are 
as follows:

 * Layer fc1,  number of neurons: _state_size_ x _fc1_units_, 
 * Layer fc2,  number of neurons: _fc1_units_ x _fc2_units_,
 * Layer fc3,  number of neurons: _fc2_units_ x _action_size_,
 
where _state_size_ = 37, _action_size_ = 8, _fc1_units_ and _fc2_units_
are the input params.
 
### Output of training

This is the typical output of training sessions:

 fc1_units:  96 , fc2_units:  80
 train_numb:  0 eps_start:  0.989
 Episode: 606, elapsed: 0:09:13.163297, Avg.Score: 13.01,  score 14.0, How many scores >= 13: 54, eps.: 0.09
 terminating at episode : 606 ave reward reached +13 over 100 episodes
 ![1][image2]      
 
 fc1_units:  96 , fc2_units:  96
 train_numb:  1 eps_start:  0.988
 Episode: 586, elapsed: 0:08:38.071115, Avg.Score: 13.01,  score 16.0, How many scores >= 13: 60, eps.: 0.09
 terminating at episode : 586 ave reward reached +13 over 100 episodes
 ![2][image3]   
 
 fc1_units:  96 , fc2_units:  104
 train_numb:  2 eps_start:  0.992
 Episode: 604, elapsed: 0:09:08.154314, Avg.Score: 13.02,  score 19.0, How many scores >= 13: 61, eps.: 0.09
 terminating at episode : 604 ave reward reached +13 over 100 episodes
 ![3][image4]   

 fc1_units:  96 , fc2_units:  88
 train_numb:  3 eps_start:  0.988
 Episode: 603, elapsed: 0:08:52.085974, Avg.Score: 13.04,  score 20.0, How many scores >= 13: 60, eps.: 0.09
 terminating at episode : 603 ave reward reached +13 over 100 episodes
 ![4][image5]   

 fc1_units:  80 , fc2_units:  80
 train_numb:  4 eps_start:  0.992
 Episode: 614, elapsed: 0:09:20.893089, Avg.Score: 13.01,  score 13.0, How many scores >= 13: 58, eps.: 0.08
 terminating at episode : 614 ave reward reached +13 over 100 episodes 
 ![5][image6]    

### Testing sessions

We run testing for each file _weights_i.trn_, where i = 0,1,2,...
The testing procedure is implemented by the function **checkWeights**.
**Important**: the function **checkWeights** constructs again the agent with 
the parameters _fc1_units_ and _fc2_units_ corresponding to the fiven weights file.
The environment _env_  is reset with the paarmeter _train_mode_=_False_.

### Test average score

The function **checkWeights** calculates the accumulated score for 
the episode generated by Unity environment _env_.
For each testing session, we run **checkWeights** several times (=6 in this version) 
to get the average score for the given set of parameters. 

### Output of testing 

=========================================================   
Train: 0, Test: 0, Episode: 606, fc1_units: 96, fc2_units: 80, eps_start: 0.989, Score: 20.0
Train: 0, Test: 1, Episode: 606, fc1_units: 96, fc2_units: 80, eps_start: 0.989, Score: 14.0
Train: 0, Test: 2, Episode: 606, fc1_units: 96, fc2_units: 80, eps_start: 0.989, Score: 10.0
Train: 0, Test: 3, Episode: 606, fc1_units: 96, fc2_units: 80, eps_start: 0.989, Score: 19.0
Train: 0, Test: 4, Episode: 606, fc1_units: 96, fc2_units: 80, eps_start: 0.989, Score: 17.0
Train: 0, Test: 5, Episode: 606, fc1_units: 96, fc2_units: 80, eps_start: 0.989, Score: 14.0 
       
    Average Score:  15.6666666667 ( **the best result**)
       
=========================================================   
Train: 1, Test: 0, Episode: 586, fc1_units: 96, fc2_units: 96, eps_start: 0.988, Score: 13.0
Train: 1, Test: 1, Episode: 586, fc1_units: 96, fc2_units: 96, eps_start: 0.988, Score: 23.0
Train: 1, Test: 2, Episode: 586, fc1_units: 96, fc2_units: 96, eps_start: 0.988, Score: 10.0
Train: 1, Test: 3, Episode: 586, fc1_units: 96, fc2_units: 96, eps_start: 0.988, Score: 10.0
Train: 1, Test: 4, Episode: 586, fc1_units: 96, fc2_units: 96, eps_start: 0.988, Score: -1.0
Train: 1, Test: 5, Episode: 586, fc1_units: 96, fc2_units: 96, eps_start: 0.988, Score: 6.0

    Average Score:  10.1666666667     
    
=========================================================  
Train: 2, Test: 0, Episode: 604, fc1_units: 96, fc2_units: 104, eps_start: 0.992, Score: 19.0
Train: 2, Test: 1, Episode: 604, fc1_units: 96, fc2_units: 104, eps_start: 0.992, Score: 11.0
Train: 2, Test: 2, Episode: 604, fc1_units: 96, fc2_units: 104, eps_start: 0.992, Score: 13.0
Train: 2, Test: 3, Episode: 604, fc1_units: 96, fc2_units: 104, eps_start: 0.992, Score: 4.0
Train: 2, Test: 4, Episode: 604, fc1_units: 96, fc2_units: 104, eps_start: 0.992, Score: 5.0
Train: 2, Test: 5, Episode: 604, fc1_units: 96, fc2_units: 104, eps_start: 0.992, Score: 1.0

    Average Score:  8.83333333333
    
=========================================================   
Train: 3, Test: 0, Episode: 603, fc1_units: 96, fc2_units: 88, eps_start: 0.988, Score: 15.0
Train: 3, Test: 1, Episode: 603, fc1_units: 96, fc2_units: 88, eps_start: 0.988, Score: 11.0
Train: 3, Test: 2, Episode: 603, fc1_units: 96, fc2_units: 88, eps_start: 0.988, Score: 15.0
Train: 3, Test: 3, Episode: 603, fc1_units: 96, fc2_units: 88, eps_start: 0.988, Score: 11.0
Train: 3, Test: 4, Episode: 603, fc1_units: 96, fc2_units: 88, eps_start: 0.988, Score: 17.0
Train: 3, Test: 5, Episode: 603, fc1_units: 96, fc2_units: 88, eps_start: 0.988, Score: 13.0

   Average Score:  13.6666666667 
   
=========================================================  
Train: 4, Test: 0, Episode: 614, fc1_units: 80, fc2_units: 80, eps_start: 0.992, Score: 19.0
Train: 4, Test: 1, Episode: 614, fc1_units: 80, fc2_units: 80, eps_start: 0.992, Score: 15.0
Train: 4, Test: 2, Episode: 614, fc1_units: 80, fc2_units: 80, eps_start: 0.992, Score: 13.0
Train: 4, Test: 3, Episode: 614, fc1_units: 80, fc2_units: 80, eps_start: 0.992, Score: 13.0
Train: 4, Test: 4, Episode: 614, fc1_units: 80, fc2_units: 80, eps_start: 0.992, Score: 6.0
Train: 4, Test: 5, Episode: 614, fc1_units: 80, fc2_units: 80, eps_start: 0.992, Score: 12.0

   Average Score:  13.0

### Credit

Most of the code is based on Udacity's DQN code.
