## Policies and Value Functions

Now, we discuss how do we measure "how good" it is for an agent to choose a given action in a specific state. A policy is the agent's behavior. A value function is a prediction of the future reward that is used to evaluate the goodness/badness of states.

### Policies

A **policy**, $\pi: S \rightarrow A$, is a function that maps each state to an action. 
* A deterministic policy: $a = \pi(s)$ describes how to get from some state $s$ to some action $a$
* A stochastic policy: $\pi(a|s) = P[A_t=a|S_t=s]$ is a distribution over actions given states

The **optimal policy** is a policy $\pi^*$ that has an expected return that is greater than or equal to the expected return or utility for all states as compared to all policies.

### Value Functions 

Value functions are functions of states or of state-action pairs that estimate how good it is for an agent to be in a specific state or how good a specific action is in a given state.

The **state-value function** for policy $\pi$ is $v_\pi$ is the expected return an agent starting at state $s$ at time $t$ that follows policy $\pi$ thereafter.[^1]
$$v_\pi(s) = E_\pi[G_t | S_t = s]$$

The **action-value function** for policy $\pi$ is $q_\pi$ is the expected return from starting at state $s$ at time $t$ taking action $a$ that follows policy $\pi$ after. 
$$q_\pi(s, a) = E_\pi [ G_t | S_t = s, A_t = a]$$
This is also known as the **Q-function**, and the output from the function is called a **Q-value**, where Q represents the quality of a given action in a given state.

[^1]: Recall, $G_t = \displaystyle\sum_{k=0}^\infty \gamma^k R_{t+k+1}$

---
*Adapted from UC Berkeley's CS 188: Introduction to Artificial Intelligence, Spring 2022 [Note 8](https://inst.eecs.berkeley.edu/~cs188/sp22/assets/notes/n8_sp22.pdf) and Deep Lizard's [Policies and Value Functions Article](https://deeplizard.com/learn/video/eMxOGwbdqKY)*