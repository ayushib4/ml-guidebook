## Optimality

### Optimal Value Function
The optimal value function outlines the best possible performance in an MDP, and this is why an MDP is effectively solved when we know the optimal value function. <br>
The **optimal state-value function** $v_*(s)$ is the maximum value function over all policies: 
$$v_*(s) = \max_\pi v_\pi (s)$$

The **optimal action-value function** $q_*(s, a)$ is the maximum action-value function over all policies: 
$$q_*(s,a) = \max_\pi q_\pi(s, a)$$

### Optimal Policy
Before we consider optimality, we will first introduce this notion of what makes a policy better than another. A policy $\pi$ is better than a policy $\pi'$ if the following holds: 
$$\pi \geq \pi' \text{ if } v_\pi(s) \geq v_{\pi'} (s), \forall s \in S$$

> <span style="color: #FF5733; font-weight: bold">💡 Theorem</span><br>
<span style="color: black">For any MDP, </span>
*   <span style="color: black"> There exists an optimal policy $\pi_*$ that is better than or equal to all other policies: $\pi_* \geq \pi, \forall \pi$ </span>
*   <span style="color: black"> All optimal policies achieve the optimal value function, $v_{\pi_*}(s) = v_*(s)$</span>
*   <span style="color: black"> All optimal policies achieve the optimal action-value function, $q_{\pi_*}(s, a) = q_*(s, a)$</span>

### Finding an Optimal Policy

Recall that there is always a deterministic optimal policy for any MDP. We will now describe an algorithm to find one:
$$
\pi_*(a|s) = \begin{cases}
   1 &\text{if } a = \underset{a \in A}{\arg\max} \text{ }q_* (s, a) \\
   0 &\text{otherwise} 
\end{cases}
$$

You might be wondering, *wow! once we have $q_*$, we can solve any MDP! But, wait...how do we get $q_*$ to begin with?* And, that's a great question. For that, we'll introduce the Bellman Optimality Equation.

### Bellman Optimality Equation

For $v_*$, we define the following relationship:
$$v_*(s) = \underset{a}{\max} \text{ } q_*(s, a)$$
Intuitively, this function is saying, at a particular state, we look ahead to all the possible actions we can possibly take, and we choose the action that yields the greatest expected return&mdash;which is just the max of all the Q-values. 

For $q_*$, we define the following relationship:
$$ q_*(s, a) = \mathcal{R}_x^a + \gamma \sum_{s' \in S} \mathcal{P}_{ss'}^a v_*(s') $$
Intuitively, we have the immediate reward from taking the given action, and then we sum over the probabilities of starting in the current state and ending up in a different state multiplied by the value function of each ending state.

We can now introduce recursive relationships for both $q_*$ and $v_*$:
$$v_*(s) = \underset{a}{\max} \text{ } \mathcal{R}_s^a + \gamma \sum_{s' \in S} \mathcal{P}_{ss'}^a v_*(s') $$
$$q_*(s, a) = \mathcal{R}_s^a + \gamma \sum_{s' \in S} \mathcal{P}_{ss'}^a \underset{a'}{\max} \text{ } q_*(s', a')$$

---
*Adapted from David Silver's [Markov Decision Processes](https://www.davidsilver.uk/wp-content/uploads/2020/03/MDP.pdf)*