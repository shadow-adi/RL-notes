# RL-notes
# Monte Carlo Methods in Reinforcement Learning

## What is Monte Carlo?

**Monte Carlo** is a model-free reinforcement learning technique that uses repeated random sampling to obtain numerical results. It is used when we have a simulation model of the environment and can only learn by interacting with it.

The term "Monte Carlo" applies to any estimation method that relies on a significant random component. For example, to find the probability of each outcome on an unfair dice, we roll it many times (say n times) and count how many times each outcome appears. The probability of outcome i = (number of times i appears) / n.

### Key Characteristics

Monte Carlo methods have these important features:

- **Model-free**: Does not require complete knowledge of the environment
- **No prior knowledge needed**: Does not require knowing the environment's dynamics in advance
- **Requires only sample transitions**: Unlike Dynamic Programming (DP), it doesn't need complete probability distributions of all possible transitions
- **Experience-based**: Learns from sample sequences of states, actions, and rewards from actual or simulated interactions
- **Can achieve optimal behavior**: Even without a complete model of the environment

## Monte Carlo Prediction

Monte Carlo methods update value estimates and policies after each episode completes, not after each step.

### Episodic Tasks

We assume experience is divided into **episodes** where:

- All episodes eventually end, regardless of which actions are selected
- Value estimates and policies only update after an episode completes

### Visits to States

When estimating the value of a state s under policy π:

- A **visit to state s** occurs each time state s appears in an episode
- A state may be visited multiple times in the same episode
- The **first visit to state s** is the first time it appears in that episode

## Monte Carlo Policy Iteration

Monte Carlo works similarly to policy iteration with two main steps:

### Step 1: Policy Evaluation

Estimate the **action-value function** (Q-value) for each state-action pair (s, a) under a given policy:

- Average all the returns that start from state-action pair (s, a) over many episodes
- Q(s,a) = average of all returns starting from (s, a)
- With enough samples, this provides precise estimates of Q(s, a) for all state-action pairs

### Step 2: Policy Improvement

Improve the policy using a greedy approach based on Q-values:

- For each state s, choose the action that maximizes Q(s, a)
- π(s) = argmax_a Q(s, a)
- This means selecting the action with the highest estimated value

## Monte Carlo Algorithm

1. **Initialize**: Create a random policy π
2. **Policy Evaluation** (repeat many times):
   - Start an episode and observe the initial state s
   - Follow the current policy π to select actions and complete the episode
   - Record the total return (reward) R(s, a) for each state-action pair visited
   - Update Q(s, a) = average of all R(s, a) for that pair
3. **Policy Improvement**:
   - Update the policy: π(s) = argmax_a Q(s, a)
4. **Repeat**: Continue steps 2 and 3 until the policy π converges to the optimal policy π*

## Returns and Value Estimation

**Returns** represent the total discounted rewards obtained from a particular state onwards. Monte Carlo methods estimate value functions by averaging returns across many episodes.

## Types of Monte Carlo Methods

There are two main variants based on how returns are averaged:

### First-Visit MC

- Averages returns only for the **first time** state s is visited in each episode
- Estimates v_π(s) as the average of returns following first visits to s

### Every-Visit MC

- Averages returns for **every time** state s is visited in each episode
- Estimates v_π(s) as the average of returns following all visits to s (including repeat visits within the same episode)

---

**Summary**: Monte Carlo methods learn from complete episodes by averaging returns to estimate value functions. They work well when you can simulate or interact with an environment but don't have a complete model of it. The two main variants differ in whether they average only the first visit or all visits to a state within episodes.
