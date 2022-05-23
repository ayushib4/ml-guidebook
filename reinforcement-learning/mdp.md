## Markov Decision Processes (MDPs)

An agent that is placed in an environment where there are multiple possible successor states from a single action in some state is a nondeterministic action. Think about a card game like poker where the randomness of dealing cards can introduce uncertainty into the succeeding actions a player might take. Problems that have an inherent degree of uncertainty are **nondeterministic search problems**, and they can be solved with **Markov Decision Processes**.

### Components of an MDP

* Agent &rarr; the decision maker
* Environment &rarr; where the agent lives
* Set of States $S$ &rarr; the representation of the environment at a given time
    * A start state
    * 1 or more terminal states &rarr; a state where once the agent arrives, it can no longer perform any actions for more rewards
* Set of Actions $A$ &rarr; what the agent decides to do at a state
* Reward $R_t$ &rarr; a scalar feedback signal that indicates how well an agent is doing at timestep $t$
* **State Transition Probability** &rarr; a probability function that represents the probability that an agent takes an action $a \in A$ from a state $s \in S$ and ends up in state $s'$
$$ \mathcal{P}_{s,s'}^a = P[S_{t+1} = s' | S_t = s, A_t = a]$$
    * **State transition matrix** $\mathcal{P}$ defines transition probabilities from all states $s$ to all successor states $s'$ (each row sums to 1)
    $$
    \text{to} \\
    \mathcal{P} =     \text{from} 
    \begin{bmatrix}
    
    P_{11} & \cdots & P_{1n} \\
    & \vdots & \\
    P_{n1} & \cdots & P_{nn} \\
    \end{bmatrix}$$
* **Reward Function** &rarr; predicts the next (immediate) reward
$$ \mathcal{R}_s^a =E[R_{t+1} | S_t = s, A_t = a]$$

> <span style="color: #FF5733; font-weight: bold">💡 Reward Hypothesis</span><br>
<span style="color: black">All goals can be described by the maximization of expected cumulative reward </span>

### Return and Discounting

We can view the agent's states through discrete timesteps where at timestep $t$, an agent is at state $s_t$ and takes action $a_t$. Starting at timestep 0, we can construct the following model:
$$s_0 \xrightarrow{a_0} s_1 \xrightarrow{a_1} s_2 \xrightarrow{a_2} \cdots$$
The **return** $G_t$ is the total reward from timestep $t$:
$$G_t = R_{t+1} + R_{t+1} + \cdots = \displaystyle\sum_{k=0}^\infty R_{t+k+1}$$

It may seem like if you keep choosing the same optimal state-action-reward set that you can get your utility function to equal a value that grows unboundedly. However, we now introduce this idea of finite horizons and discount factors. A **finite horizon** is a "lifetime" for agents that limits the number of timesteps to maximize reward before the agent is terminated. A **discount factor** or **discount rate**, $\gamma$, is a number between 0 and 1 that is the rate for which we discount future rewards ($\gamma$ close to 0 leads to myopic evaluation; $\gamma$ close to 1 leads to far-sighted evaluation). 

Now, we can say that our agent's goal is to maximize the **total discounted reward**:

$$G_t = R_{t+1} + \gamma R_{t+1} + \cdots = \displaystyle\sum_{k=0}^\infty \gamma^k R_{t+k+1} \leq \displaystyle\sum_{t=0}^\infty \gamma^t R_{max} = \frac{R_{max}}{1-\gamma}$$

> <details>
<summary> <span style="color: #28B4A9; font-weight: bold"> 🎲 Why do we use discounted rewards? (click me) </span> </summary>
<span style="color: black">Mathematically convenient to discount rewards, avoids infinite returns in cyclic Markov processes, uncertainty about the future may not be fully represented, animal/human behaviors show preference for immediate rewards, etc.
</span>
</details>


 ### Memoryless Property

 MDPs are **memoryless**, meaning that only the current state affects the future state, and the future and the past are conditionally independent. Mathematically, we can express this as: $T(s, a, s') = P(s' | s, a) $. In other words, the probability of arriving to state $s'$ at time $t+1$ only depends on the current state at time $t$ and not any of the previous states.
 The future is independent of the past given the present.

> <span style="color: #FF5733; font-weight: bold">💡 Markov or Memoryless Property</span><br>
<span style="color: black">The future is independent of the past given the present  <br>
$P[S_{t+1} | S_t] = P[S_{t+1} | S_1, \cdots S_t]$ </span>

---
*Adapted from UC Berkeley's CS 188: Introduction to Artificial Intelligence, Spring 2022 [Note 8](https://inst.eecs.berkeley.edu/~cs188/sp22/assets/notes/n8_sp22.pdf)*