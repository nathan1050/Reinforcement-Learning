# Reinforcement Learning 
Building an Agent that plays Space Invaders after learning it through playing multiple games
 
## Introduction 
Artificial Intelligence and since fiction has always awed human beings with the prospect of creating humanoid beings capable of complex tasks. Reinforcement Learning will deliver what Artificial Intelligence promised. Learning to control agents directly from high-dimensional sensory inputs like vision and speech is one of the longest challenges of Reinforcement Learning. Most successful RL applications that operate on these domains have relied on hand- crafted features combined with linear value functions or policy representations. Clearly, the performance of such systems heavily relies on the quality of the feature representation.

## Background 
I’m considering tasks in which an agent interacts with an environment, in this case the emulator of the game Space Invaders, in a sequence of actions, observations and rewards. At each time- step the agent selects an action at from the set of legal game actions. The action is passed to the emulator and modifies its internal state and the game score. The emulator’s internal state is not observed by the agent; instead it observes an image from the emulator, which is a vector of raw pixel values representing the current screen. In addition it receives a reward representing the change in game score. The game score may depend on the whole prior sequence of actions and observations; feedback about an action may only be received after many thousands of time- steps have elapsed.
The goal of the agent is to interact with the emulator by selecting actions in a way that maximizes future rewards.

## Action Space 
The action spaces are the valid moves or actions the agent can take. There are six discrete actions available: do nothing, fire at 90 degrees, move left, move right, fire right, and fire left.

['NOOP', 'FIRE', 'LEFT', 'RIGHT', 'LEFTFIRE', 'RIGHTFIRE'].  

## Model Architecture 
Describing the architecture used for the game. The input to the neural network consists is an 84 × 84 × 4 image produced by φ. The first hidden layer convolves 32, 8 × 8 filters with stride4 with the input image and applies a rectifier nonlinearity (Relu) activation function. The second hidden layer convolves 64, 4 × 4 filters with stride 2, again followed by a rectifier nonlinearity. These are then passed on to a flatten layer and then a dense layer. The output layer is a fully connected linear layer with a single output for each valid action.  

The model architecture is shown below:  

![Alt text](/img/1.jpeg "Model_train") 

## Building the Agent 
Over the past years, deep learning has contributed to dramatic advances in scalability and performance of machine learning. The reinforcement agent I’m using is a DQN Agent. The dueling (Dueling DQN) architecture, explicitly separates the representation of state values and (state-dependent) action advantages. The dueling architecture consists of two streams that represent the value and advantage functions, while sharing a common convolutional feature learning module. The two streams are combined via a special aggregating layer to produce an estimate of the state-action value function Q.  

Q(s,a) = V(s) + A(s,a)

A Policy is what the agent does to accomplish its goal, given its state. I’ve tested the sample space of moves of my agent based on two Policies.

1. LinearAnnealedPolicy with EpsGreedyQPolicy
![Alt text](/img/2.jpeg "Linear")

2. BoltzmanQPolicy
![Alt text](/img/3.jpeg "Boltzman")

## Training
In supervised learning, one can easily track the performance of a model during training by evaluating it on the training and validation sets. In reinforcement learning, however, accurately evaluating the progress of an agent during training can be challenging. The evaluation metric is the total reward the agent collects in an episode or game averaged over a number of games. The average total reward metric tends to be very noisy because small changes to the weights of a policy can lead to large changes in the distribution of states the policy visits.

My best model was trained with the LinearAnnealedPolicy with EpsGreedyQPolicy for 50,000 steps.

![Alt text](/img/4.jpeg "Training")

## Testing
![Alt text](/img/5.png "Testing")

This is a graph displaying running the model for 100 games

## Conclusion

Reinforcement learning is a very good and powerful technique to train an agent/model.
Although it is a good technique, it requires a lot of time to become really good. Experts recommend at least a week of training for a simple game like Space Invaders.
There are a lot of other industries and areas where this set of learning is in use and changing the game like Computer Networking, Inventory Management, Vehicle Navigation and many many more.



