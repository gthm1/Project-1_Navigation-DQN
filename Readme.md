
# Project 1: Navigation

### Overview of the project

In this project, we will train a agent to navigate the world and collect yellow bananas while avoiding blue bananas. The agent will be rewarded +1 for every yellow banana it collects and -1 for every blue one.

We have 37 possible dimensions and contains the agents velocity along with ray-based perception of objects around the agent's forward direction. Given this information, the agent has to learn how to best select actions. Four discrete actions are available, corresponding to:

0 - move forward
1 - move backward
2 - turn left
3 - turn right 

The task is episodic, and in order to solve the environment, the agent must get an average score of +13 over 100 consecutive episodes.


### Requirement Gathering And Running Project

1) To run this project on your local machine you should have certain packages on your system. You can find them in requirements.txt. They can be installed using the command "pip install requirements.txt".

2) You can  download the required environment using the links below:
       Windows_32bit : https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86.zip
       Windows_64bit : https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip
       linux : https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip
       Mac : https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip

3) Then run the cells in Navigation.ipynb, then you will be able to train the agent which can solve the task of collecting bananas.