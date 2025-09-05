# Cart-Pole-Balancing
# **Theoretical Explanation of CartPole DQN Project**

---

## **1. Project Purpose**

The purpose of this project is to **develop a reinforcement learning agent** that can balance a pole on a moving cart in the **CartPole-v1** environment.

Key objectives:

1. Understand how **Reinforcement Learning (RL)** algorithms interact with an environment to maximize cumulative reward.
2. Implement a **Deep Q-Network (DQN)** to approximate the action-value function for a continuous state space.
3. Apply **experience replay** and **target networks** to stabilize training.
4. Demonstrate the agent’s ability to learn a policy that consistently keeps the pole upright.

---

## **2. Reinforcement Learning Overview**

Reinforcement Learning is a type of machine learning where an **agent learns by interacting with an environment**:

* **State (s):** The environment's current condition (e.g., cart position, pole angle).
* **Action (a):** A decision the agent makes (move left or right).
* **Reward (r):** Feedback signal for each action (+1 for keeping pole upright).
* **Policy (π):** Strategy mapping states → actions to maximize long-term reward.
* **Objective:** Maximize **cumulative discounted reward**:

$$
R_t = r_t + \gamma r_{t+1} + \gamma^2 r_{t+2} + \dots
$$

* **Discount factor (γ):** Determines how much future rewards are valued relative to immediate rewards.

---

## **3. Deep Q-Network (DQN)**

**Problem:** CartPole has **continuous state variables**, so a simple Q-table is infeasible.

**Solution:** Use a **neural network** to approximate the **Q-value function** $Q(s, a)$:

$$
Q(s, a; \theta) \approx Q^*(s, a)
$$

Where:

* $\theta$ = neural network weights.
* Input = current state vector (cart position, velocity, pole angle, angular velocity).
* Output = predicted Q-values for each possible action.

**Key DQN concepts implemented in this project:**

1. **Policy Network**

   * Predicts Q-values for the current state.
   * Guides the agent in choosing the **best action**.

2. **Target Network**

   * A frozen copy of the policy network.
   * Provides **stable Q-targets** during training:

$$
y = r + \gamma \max_{a'} Q_{\text{target}}(s', a')
$$

3. **Experience Replay**

   * Stores past experiences `(state, action, reward, next_state, done)` in a **buffer**.
   * Randomly samples minibatches to train the network.
   * Breaks correlation between consecutive experiences → **stabilizes learning**.

4. **Epsilon-Greedy Exploration**

   * Initially, agent chooses actions randomly (**exploration**).
   * Over time, reduces randomness to exploit learned policy (**exploitation**).

---

## **4. Training Process**

1. **Initialize environment and networks**.
2. For each episode:

   * Observe current state.
   * Choose action using **ε-greedy policy**.
   * Apply action → receive reward and next state.
   * Store experience in **replay buffer**.
   * Sample random minibatch → compute **loss** between predicted Q-values and target Q-values.
   * Update **policy network weights** via gradient descent.
   * Periodically update **target network**.
3. Repeat for **many episodes** until agent consistently balances the pole.

**Outcome:** The policy network learns to choose actions that **maximize cumulative reward**, allowing the agent to balance the pole for the maximum number of steps.

---

## **5. Why This Project is Important**

* Demonstrates understanding of **core RL concepts**: states, actions, rewards, policies, and value functions.
* Bridges **deep learning** and **reinforcement learning**.
* Implements **modern RL techniques**: DQN, target networks, replay buffer, ε-greedy exploration.
* Forms a foundation for more complex RL projects like **Atari games, robotics control, or autonomous navigation**.
