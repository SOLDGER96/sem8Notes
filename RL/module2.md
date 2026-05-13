### **Question: Enlist components of MDP model and explain in detail? (5 marks)**

**Answer:**

**1. Introduction to MDP:**
A **Markov Decision Process (MDP)** is a mathematical framework used in Reinforcement Learning to describe an environment for decision-making. It models situations where outcomes are partly random (controlled by the environment) and partly under the control of a decision-maker (the agent).

An MDP is formally defined as a tuple of five components: **$(S, A, P, R, \gamma)$**.

**2. Detailed Components of the MDP Model:**

* **1. Set of States ($S$):**
    * **Explanation:** It is a finite set of all possible situations or configurations the environment can be in. A state $s \in S$ provides the agent with all the necessary information about the environment at time step $t$ to make a decision.
    * *Example:* In a game of chess, the state is the specific arrangement of all pieces on the board at a given turn.

* **2. Set of Actions ($A$):**
    * **Explanation:** It is a finite set of all valid moves or decisions the agent can make. In some models, the available actions depend on the specific state the agent is currently in, denoted as $A(s)$.
    * *Example:* In a maze-solving robot, the actions might be {*Move North, Move South, Move East, Move West*}.

* **3. Transition Probability Function ($P$ or $P_a(s, s')$):**
    * **Explanation:** This defines the *dynamics* of the environment. It specifies the probability that taking action $a$ in the current state $s$ at time $t$ will lead to the next state $s'$ at time $t+1$. 
    * **Formula:** $P_a(s, s') = Pr(S_{t+1} = s' \mid S_t = s, A_t = a)$
    * *Significance:* It captures the \"stochastic\" (random) nature of the environment. If the environment is completely deterministic, this probability is exactly $1$ for a specific next state and $0$ for all others.

* **4. Reward Function ($R$ or $R_a(s, s')$):**
    * **Explanation:** It is the immediate numerical feedback (expected reward) received by the agent after transitioning from state $s$ to state $s'$ due to action $a$. 
    * **Formula:** $R_a(s, s') = \mathbb{E}[R_{t+1} \mid S_t = s, A_t = a, S_{t+1} = s']$
    * *Significance:* It defines the ultimate goal of the problem. The agent's objective is to maximize the cumulative sum of these rewards over time.

* **5. Discount Factor ($\gamma$):**
    * **Explanation:** A parameter strictly between $0$ and $1$ ($0 \le \gamma \le 1$) that determines the importance of future rewards compared to immediate rewards.
    * *Significance:* * If $\gamma$ is close to $0$: The agent becomes \"myopic\" and only cares about immediate rewards.
        * If $\gamma$ is close to $1$: The agent becomes \"farsighted\" and values long-term future rewards almost as much as immediate ones.

---

### **Question: What is optimal policies and explain optimal value function (q*)? (5 marks)**

**Answer:**

**1. Definition of OPTIMAL POLICY ($\pi^*$):**
* **Concept:** A policy ($\pi$) is a mapping from states to actions (a strategy). A policy $\pi$ is considered better than or equal to another policy $\pi'$ if its expected cumulative reward is greater than or equal to that of $\pi'$ for *every* possible state. 
* **Optimal Policy:** An optimal policy (denoted as $\pi^*$) is the absolute best strategy an agent can follow. It is a policy that yields the highest possible expected return among all conceivable policies. 
* **Note:** There can be more than one optimal policy for a given problem, but all optimal policies will share the exact same optimal value functions.

**2. Explanation of OPTIMAL ACTION-VALUE FUNCTION ($q^*$):**
* **Concept:** The action-value function, $q_\pi(s, a)$, calculates the expected return starting from state $s$, taking action $a$, and strictly following policy $\pi$ thereafter. 
* **The Optimal Function ($q^*$):** The **optimal action-value function** (denoted as $q^*(s, a)$) calculates the expected return starting from state $s$, taking action $a$, and thereafter following an *optimal policy* ($\pi^*$). 
* It outputs the maximum possible value achievable under *any* policy for that specific state-action pair.
* **Mathematical Definition:**
    $$q^*(s, a) = \max_{\pi} q_{\pi}(s, a)$$

**3. Relationship to Optimal Policy (How the agent uses $q^*$):**
If an agent accurately learns the optimal action-value function $q^*(s, a)$, finding the optimal policy becomes trivial. The agent simply looks at its current state $s$ and chooses the action $a$ that has the highest $q^*$ value. This is known as acting greedily with respect to $q^*$.

**4. Bellman Optimality Equation for $q^*$ (Topper's Addition for Max Marks):**
The optimal action-value function must satisfy the Bellman Optimality Equation. It states that the value of taking action $a$ in state $s$ under an optimal policy must equal the expected immediate reward plus the discounted expected maximum value of the next state:
$$q^*(s, a) = \mathbb{E} \left[ R_{t+1} + \gamma \max_{a'} q^*(S_{t+1}, a') \mid S_t = s, A_t = a \right]$$

Where:
* $R_{t+1}$ = Immediate expected reward.
* $\gamma$ = Discount factor.
* $\max_{a'} q^*(S_{t+1}, a')$ = The value of the absolute best action available in the next state.


---

### **Question: Describe the components of an MDP, including states, actions, transition probabilities, and rewards. (10 marks)**

**Answer:**

**1. Introduction to Markov Decision Process (MDP):**
A **Markov Decision Process (MDP)** is a mathematical framework used to model decision-making in situations where outcomes are partly random and partly under the control of a decision-maker (the agent). It is the fundamental formalization of the Reinforcement Learning (RL) problem. 

An MDP is formally defined as a tuple of 5 core components: **$(S, A, P, R, \gamma)$**. 

Below is the detailed explanation of each component:

---

**2. Detailed Components of the MDP Model:**

**I. STATES ($S$)**
* **Definition:** The state space $S$ is a finite set of all possible situations, configurations, or observations that the environment can be in. 
* **Explanation:** At each discrete time step $t$, the agent receives a representation of the environment's current condition, denoted as $S_t \in S$. The state must contain all the necessary information required for the agent to make an optimal decision.
* **The Markov Property:** A critical requirement of an MDP is that the state must satisfy the *Markov Property*. This means the current state captures all relevant information from the history. The future depends *only* on the current state and action, completely independent of the past sequence of states that led there.
* **Example:** In a chess game, the state is the exact coordinate position of every piece on the board at that specific turn.

**II. ACTIONS ($A$)**
* **Definition:** The action space $A$ is a finite set of all valid moves or choices available to the agent. 
* **Explanation:** At time step $t$, the agent selects an action $A_t \in A$. In some complex environments, the set of available actions might depend entirely on the specific state the agent is currently in, which is denoted as $A(s)$.
* **Example:** For a self-driving car, the action space might include {*Steer Left, Steer Right, Accelerate, Brake*}.

**III. TRANSITION PROBABILITIES ($P$ or $p(s' | s, a)$)**
* **Definition:** This component defines the *dynamics* or the \"rules\" of the environment. It defines the probability of transitioning to a new state $s'$ given that the agent took action $a$ in the current state $s$.
* **Explanation:** Most real-world environments are *stochastic* (probabilistic). If a robot tries to move forward, its wheels might slip, causing it to end up in an unintended state. The transition probability mathematically captures this uncertainty.
* **Mathematical Formula:** $$P_a(s, s') = Pr(S_{t+1} = s' \mid S_t = s, A_t = a)$$

  *(The probability that the next state is $s'$ given the current state $s$ and current action $a$).*
* **Constraint:** The sum of probabilities of transitioning to all possible next states must equal 1: $\sum_{s' \in S} P_a(s, s') = 1$.

**IV. REWARDS ($R$ or $R(s, a, s')$)**
* **Definition:** The reward function provides a scalar numerical feedback signal (the immediate reward) received by the agent after transitioning from state $s$ to state $s'$ due to action $a$.
* **Explanation:** The reward signal defines the ultimate *goal* of the problem. Every time the agent takes an action, the environment responds with a reward $R_{t+1}$. The agent's sole objective is to maximize the *cumulative* reward over time, not just the immediate reward.
* **Mathematical Formula:**
  $$R_a(s, s') = \mathbb{E}[R_{t+1} \mid S_t = s, A_t = a, S_{t+1} = s']$$

* **Example:** In a Pac-Man game, eating a dot yields a reward of $+10$, being caught by a ghost yields $-100$, and hitting a wall yields $0$.

---

**3. The 5th Component (For Completeness & Extra Marks):**

**V. DISCOUNT FACTOR ($\gamma$)**
* **Definition:** A parameter strictly between $0$ and $1$ ($0 \le \gamma \le 1$) used to determine the present value of future rewards.
* **Explanation:** It controls the agent's foresight. 
    * If $\gamma = 0$: The agent is extremely short-sighted and only tries to maximize the very next immediate reward.
    * If $\gamma$ approaches $1$: The agent is far-sighted and values long-term future rewards heavily, ensuring the algorithm converges efficiently in continuous tasks.

**Summary of Interaction:**
At time step $t$, the agent observes State $S_t$ from the environment and chooses an Action $A_t$. The environment, using its Transition Probabilities $P$, moves to a new State $S_{t+1}$ and emits a Reward $R_{t+1}$ back to the agent. The agent uses this feedback to update its policy and the cycle repeats.

---

### **Question: Imagine you're designing a simple game where a player controls a character to navigate through a maze to reach a treasure chest. The player receives a reward of +10 points upon reaching the treasure chest and -1 point for each move taken. Assume the player starts at the entrance of the maze. (10 marks)**
**1. If the player reaches the treasure chest in 15 moves, what is their total reward?**

**2. If the player reaches the treasure chest in 20 moves, what is their total reward?**

**3. What is the maximum possible reward the player can achieve in this game?**

**4. What would be the reward if the player gets stuck in the maze indefinitely?**

---

**Answer:**

**1. GIVEN DATA (PROBLEM FORMULATION)**
In Reinforcement Learning (RL) terminology, this is an episodic task. 
* **Goal Reward ($R_{goal}$):** $+10$ points (Terminal state) 
* **Step Penalty ($R_{step}$):** $-1$ point per move 
* **Total Expected Reward Formula ($G$):** The total reward is the sum of the goal reward and the accumulated step penalties. Let $N$ be the total number of moves taken.
    $$Total \ Reward = R_{goal} + (N \times R_{step})$$

    $$Total \ Reward = 10 + (N \times -1)$$

    $$Total \ Reward = 10 - N$$

---

**2. STEP-BY-STEP SOLUTIONS**

* **Sub-Question 1: Total reward for 15 moves?** 
    * *Calculation:* Substitute $N = 15$ into the formula.
    * $$Total \ Reward = 10 - 15 = -5$$

    * **FINAL ANSWER:** The total reward is **$-5$ points**. (The agent spent more points wandering the maze than the treasure was worth).

* **Sub-Question 2: Total reward for 20 moves?** 
    * *Calculation:* Substitute $N = 20$ into the formula.
    * $$Total \ Reward = 10 - 20 = -10$$

    * **FINAL ANSWER:** The total reward is **$-10$ points**.

* **Sub-Question 3: What is the maximum possible reward?** 
    * *Concept:* To maximize the overall reward, the agent must *minimize* the negative step penalties. Therefore, the maximum possible reward is strictly determined by the **shortest optimal path** from the entrance to the chest.
    * *Calculation:* Let $S_{min}$ be the absolute minimum number of moves required to solve the maze (the shortest path).
    * **FINAL ANSWER:** The maximum possible reward is mathematically represented as **$10 - S_{min}$**. *(For example, if the shortest path takes exactly 5 steps, the absolute maximum reward the player can achieve is $10 - 5 = 5$ points).*

* **Sub-Question 4: Reward if the player gets stuck indefinitely?** 
    * *Concept:* If the player is stuck indefinitely, they never reach the terminal state (the treasure chest) and never receive the $+10$ reward. However, they continue to take an infinite number of moves, accumulating a $-1$ penalty for every single step.
    * *Calculation:* As the number of moves $N \to \infty$, the total reward evaluates to $0 - \infty$.
    * **FINAL ANSWER:** The total reward would be **Negative Infinity ($-\infty$)**.

---
*(**TOPPER'S / EXAMINER'S NOTE:** This problem beautifully illustrates a core design principle in Reinforcement Learning called the **\"Step Penalty\"**. By assigning a negative reward ($-1$) to every step, the environment actively forces the RL agent to find the treasure as fast as possible. Without this negative penalty, the agent would have no incentive to take the shortest path and might wander aimlessly before finally collecting the $+10$ reward.)*