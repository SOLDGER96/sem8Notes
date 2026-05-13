### **Question: Define Temporal Difference and explain parameters of TD in detail? (5 marks)**

**Answer:**

**1. Definition of Temporal Difference (TD) Learning:**
**TEMPORAL DIFFERENCE (TD) LEARNING** is a model-free Reinforcement Learning approach where an agent learns to predict the expected value of a state directly from experience. 
The core characteristic of TD is **BOOTSTRAPPING**: the agent updates its estimate of the current state based on the immediate reward and the *estimated* value of the very next state, rather than waiting until the end of the episode to see the actual total return.

**2. The TD Update Rule (TD(0) Formula):**
$$V(S_t) \leftarrow V(S_t) + \alpha \left[ R_{t+1} + \gamma V(S_{t+1}) - V(S_t) \right]$$

**3. Detailed Explanation of TD Parameters:**
Every component in the TD formula serves a specific mathematical purpose:

* **Current State Value ($V(S_t)$):** The agent's current best guess (estimate) of the expected return starting from the current state $S_t$.
* **Next State Value ($V(S_{t+1})$):** The agent's estimated value of the state it lands in after taking an action. This is where the *bootstrapping* occurs (using an estimate to update another estimate).
* **Immediate Reward ($R_{t+1}$):** The actual numerical reward received immediately after taking an action from state $S_t$.
* **Learning Rate ($\alpha$):** (Where $0 < \alpha \le 1$). It determines how much the newly acquired information overrides the old information. A high $\alpha$ means the agent quickly discards old estimates, while a low $\alpha$ means it learns slowly but stably.
* **Discount Factor ($\gamma$):** (Where $0 \le \gamma \le 1$). It determines the present value of future rewards. It discounts the estimate of the next state ($V(S_{t+1})$) so the agent doesn't overvalue distant, uncertain futures.
* **The TD Target ($R_{t+1} + \gamma V(S_{t+1})$):** This represents the *better* estimate of the current state, consisting of the actual immediate reward plus the discounted future estimate.
* **The TD Error ($\delta_t$):** The term in the brackets $[R_{t+1} + \gamma V(S_{t+1}) - V(S_t)]$. It calculates the difference between the new, better estimate (the target) and the old estimate. If the error is positive, the state was undervalued; if negative, it was overvalued.

---

### **Question: How does TD prediction differ from Monte Carlo prediction? (5 marks)**

**Answer:**

**1. Core Conceptual Difference:**
While both are model-free methods used to evaluate a policy (prediction), they differ fundamentally in **WHEN** they update their values and **WHAT** they use as the target for the update. 
* **Monte Carlo (MC)** must wait until the absolute end of an episode to calculate the actual total return.
* **Temporal Difference (TD)** updates its values continuously, step-by-step, by guessing the future based on the next state.

**2. Comparison Table (For Max Marks in Exams):**

| Feature | Temporal Difference (TD) Prediction | Monte Carlo (MC) Prediction |
| :--- | :--- | :--- |
| **Update Timing** | Updates values **online, step-by-step** immediately after a transition. | Updates values **offline, at the end** of an entire episode. |
| **Bootstrapping** | **YES.** It updates estimates based on other estimates (guesses from a guess). | **NO.** It updates estimates based solely on the actual, fully observed return. |
| **Environment Types** | Works in both **Episodic** and **Continuing** (never-ending) environments. | Works **ONLY in Episodic** environments (must reach a terminal state). |
| **Bias vs. Variance** | Has **Low Variance** but **High Bias** (initially biased by arbitrary starting estimates). | Has **High Variance** (depends on many random actions) but **Zero Bias**. |
| **Information Speed** | Learns **faster** initially because it doesn't have to wait for an episode to end. | Learns **slower** per step, especially if episodes are extremely long. |
| **Target Formula** | Uses the **TD Target**: $R_{t+1} + \gamma V(S_{t+1})$ | Uses the **Actual Return**: $G_t = R_{t+1} + \gamma R_{t+2} + \dots$ |

**3. Summary Analogy:**
If you are predicting the final score of a cricket match:
* **Monte Carlo** waits until the match is completely over, sees the final score, and then adjusts its prediction rules for the next match.
* **Temporal Difference** adjusts its prediction after every single over, updating its final guess based on the current run rate (bootstrapping).

---

### **Question: Explain the differences between TD learning and Monte Carlo methods. Also, describe the main components and key steps involved in TD prediction algorithms. (10 marks)**

**Answer:**

#### **PART 1: Differences between Temporal Difference (TD) Learning and Monte Carlo (MC) Methods**

Both Temporal Difference (TD) and Monte Carlo (MC) methods are **model-free** Reinforcement Learning techniques used to estimate value functions from experience. However, they fundamentally differ in how and when they update their estimates.

**Comparison Table:**

| Feature | Temporal Difference (TD) Learning | Monte Carlo (MC) Methods |
| :--- | :--- | :--- |
| **Update Timing** | Updates values **online, step-by-step** immediately after transitioning to the next state. | Updates values **offline, at the end** of an entire episode. |
| **Bootstrapping** | **YES.** It updates its current estimate based on the *estimated* value of the next state (guessing from a guess). | **NO.** It updates estimates based solely on the *actual, fully observed* cumulative return. |
| **Environment Types** | Can be used in both **Episodic** (finite) and **Continuing** (infinite/never-ending) environments. | Can **ONLY** be used in **Episodic** environments (must reach a terminal state to calculate return). |
| **Bias vs. Variance** | Has **Low Variance** (depends on one random action) but **High Bias** (initially biased by arbitrary starting estimates). | Has **High Variance** (depends on many random actions in an episode) but mathematically **Zero Bias**. |
| **Learning Target** | Uses the **TD Target**: $R_{t+1} + \gamma V(S_{t+1})$ | Uses the **Actual Return**: $G_t = R_{t+1} + \gamma R_{t+2} + \dots$ |
| **Speed of Learning** | Generally learns **faster** initially because it does not have to wait for long episodes to finish before updating. | Learns **slower** per step, especially if the episodes are extremely long. |

---

#### **PART 2: Main Components of TD Prediction Algorithms**

TD Prediction (specifically TD(0)) aims to estimate the state-value function $V_\pi(s)$ for a given policy $\pi$. The main components are defined by the TD update equation:

$$V(S_t) \leftarrow V(S_t) + \alpha \left[ R_{t+1} + \gamma V(S_{t+1}) - V(S_t) \right]$$

* **Current State Value ($V(S_t)$):** The agent's current estimated value of being in state $S_t$.
* **Next State Value ($V(S_{t+1})$):** The agent's estimated value of the state it lands in after taking an action. This enables *bootstrapping*.
* **Immediate Reward ($R_{t+1}$):** The actual numerical reward received immediately after taking an action from state $S_t$.
* **Learning Rate ($\alpha$):** A parameter ($0 < \alpha \le 1$) that dictates how much the newly calculated error overrides the old value estimate.
* **Discount Factor ($\gamma$):** A parameter ($0 \le \gamma \le 1$) that determines the present value of future rewards.
* **TD Target ($R_{t+1} + \gamma V(S_{t+1})$):** The \"new, better guess\" for the value of $S_t$, consisting of the actual immediate reward plus the discounted future estimate.
* **TD Error ($\delta_t$):** Represented by $[R_{t+1} + \gamma V(S_{t+1}) - V(S_t)]$. It is the difference between the better estimate (TD Target) and the old estimate.

---

#### **PART 3: Key Steps Involved in a TD Prediction Algorithm (TD(0))**

The standard step-by-step execution of the TD(0) prediction algorithm is as follows:

* **Step 1: Initialization**
    * Initialize the value function $V(s)$ arbitrarily for all states $s \in S$ (except terminal states, which must be $0$).
    * Specify the policy $\pi$ that needs to be evaluated.
    * Set the step-size parameter $\alpha$ and discount factor $\gamma$.

* **Step 2: Episode Loop**
    * Start a new episode and initialize the starting state $S$.

* **Step 3: Step-by-Step Execution (Inner Loop)**
    * While state $S$ is not a terminal state, repeat:
        1.  **Action Selection:** Choose an action $A$ based on the current state $S$ strictly following policy $\pi$.
        2.  **Observation:** Execute action $A$ in the environment. Observe the immediate reward $R$ and the resulting next state $S'$.
        3.  **Value Update:** Update the value estimate of the previous state $S$ using the TD formula:
            $$V(S) \leftarrow V(S) + \alpha \left[ R + \gamma V(S') - V(S) \right]$$

        4.  **State Transition:** Set the current state $S$ to the new state $S'$ ($S \leftarrow S'$).

* **Step 4: Repeat**
    * Loop back to Step 2 for the next episode until the values of $V(s)$ converge to the true value function $V_\pi(s)$.


### Q. Discuss the difference between on-policy and off-policy learning. Provide examples of algorithms that fall into each category. (5 marks)
**Answer:**
**1. Introduction to the Two Policies:**
To understand the difference, we must first define the two types of policies involved in Reinforcement Learning:
* **Target Policy ($\pi$):** The policy that the agent is trying to learn and optimize (the final goal).
* **Behavior Policy ($b$):** The policy that the agent is currently using to interact with the environment and gather data (experience).

---

**2. ON-POLICY LEARNING:**
* **Definition:** In ON-POLICY learning, the agent evaluates and improves the **EXACT SAME** policy that it is using to make decisions and navigate the environment. 
* **Key Characteristic:** Target Policy == Behavior Policy ($\pi = b$).
* **How it works:** The agent learns the value of its current exploratory policy. Since it must explore to learn, the final learned policy will always have some level of exploration built into it. It learns a \"safe\" policy that accounts for its own random exploratory mistakes.
* **Examples of On-Policy Algorithms:**
    * **SARSA** (State-Action-Reward-State-Action): It evaluates the $Q$-value of the actual action taken by the current $\epsilon$-greedy policy.
    * **REINFORCE** (Standard Policy Gradient).

---

**3. OFF-POLICY LEARNING:**
* **Definition:** In OFF-POLICY learning, the agent evaluates and improves one target policy ($\pi$) while gathering data using a completely different behavior policy ($b$).
* **Key Characteristic:** Target Policy $\neq$ Behavior Policy. 
* **How it works:** The agent can use an exploratory or even completely random behavior policy to interact with the world, while simultaneously learning the absolute **OPTIMAL, DETERMINISTIC** target policy in the background. It learns what the best action is, regardless of the exploratory action it actually took.
* **Examples of Off-Policy Algorithms:**
    * **Q-LEARNING:** It updates its $Q$-values using the absolute maximum possible reward of the next state ($\max_a Q(S', a)$), assuming the greedy optimal action will be taken, even if the agent actually takes a random action next.
    * **Deep Q-Networks (DQN)**.

---

**4. KEY DIFFERENCES (Summary for Exams):**

| Feature | On-Policy Learning | Off-Policy Learning |
| :--- | :--- | :--- |
| **Data Usage (Sample Efficiency)** | **POOR:** Must learn strictly from fresh data generated by the *current* policy. Old data becomes useless. | **EXCELLENT:** Can learn from historical data, old policies, or even human demonstrations (Experience Replay). |
| **Exploration vs Exploitation** | Learns a compromised policy that factors in the cost of ongoing exploration. | Learns the absolute mathematical optimal policy while safely exploring with a separate policy. |
| **Convergence Stability** | Generally highly **STABLE** and smooth to converge. | Often **UNSTABLE**, especially when combined with Neural Networks (e.g., the \"Deadly Triad\" problem). |
| **Algorithm Analogy** | Learning to drive by analyzing your own current driving mistakes. | Learning to drive by watching a completely different person drive (or watching past recordings). |

Here are the perfect, exam-ready answers structured to help you secure full marks. 

*(Note: Your second and third questions both ask to explain the Q-Learning algorithm for TD Control. I have combined them into a single, comprehensive \"Master Answer\" that perfectly addresses both prompts and provides all necessary details for a 10-mark question.)*

---

### **Q. Define Off-policy algorithm and on-policy algorithm and identify SARSA is which type of algorithm and why? Write SARSA algorithm in detail? (10 marks)**

**Answer:**

**1. Definition of ON-POLICY and OFF-POLICY Algorithms:**
In Reinforcement Learning, the distinction between on-policy and off-policy depends on the relationship between two policies: the **Target Policy** (the policy being learned/optimized) and the **Behavior Policy** (the policy being used to interact with the environment and gather data).

* **ON-POLICY ALGORITHM:**
    * **Definition:** An algorithm that evaluates and improves the **EXACT SAME** policy that it uses to make decisions.
    * **Concept:** Target Policy = Behavior Policy. It learns the value of the policy it is currently executing, including the exploratory mistakes it makes.

* **OFF-POLICY ALGORITHM:**
    * **Definition:** An algorithm that evaluates and improves a **TARGET POLICY** (usually the optimal, greedy policy) while gathering data using a completely different **BEHAVIOR POLICY** (usually an exploratory one, like $\epsilon$-greedy).
    * **Concept:** Target Policy $\neq$ Behavior Policy. It can learn the absolute best strategy by watching other agents, using old data, or exploring randomly.

**2. Identification of SARSA:**
* **Classification:** SARSA is an **ON-POLICY** Temporal Difference (TD) control algorithm.
* **Why?** SARSA updates its action-value estimates, $Q(s, a)$, based on the action $A'$ that the agent *actually takes* in the next state $S'$ according to its current behavior policy. It does not blindly assume the agent will take the absolute best mathematical action in the future; it accounts for the fact that the agent might explore and make a sub-optimal move.

**3. The SARSA Algorithm in Detail:**
**Acronym Meaning:** The name SARSA comes from the sequence of events that make up one step of the algorithm: **S**tate, **A**ction, **R**eward, Next **S**tate, Next **A**ction ($S_t, A_t, R_{t+1}, S_{t+1}, A_{t+1}$).

**The SARSA Update Formula:**
$$Q(S, A) \leftarrow Q(S, A) + \alpha [R + \gamma Q(S', A') - Q(S, A)]$$

*(Where $\alpha$ is the learning rate, $\gamma$ is the discount factor, and $A'$ is the actual next action chosen by the policy).*

**Step-by-Step Algorithm:**
* **Step 1:** Initialize the action-value function $Q(s, a)$ arbitrarily for all states and actions (except terminal states, which must be 0).
* **Step 2:** Set parameters like learning rate ($\alpha$), discount factor ($\gamma$), and exploration rate ($\epsilon$).
* **Step 3:** Loop for each episode:
    * Initialize the starting state $S$.
    * Choose an initial action $A$ from state $S$ using a policy derived from $Q$ (e.g., **$\epsilon$-GREEDY**).
* **Step 4:** Loop for each step of the episode until $S$ is terminal:
    * Take action $A$, and observe the immediate reward $R$ and the next state $S'$.
    * Choose the next action $A'$ from the next state $S'$ using the **SAME** policy (e.g., $\epsilon$-greedy).
    * Apply the SARSA update rule: update $Q(S, A)$ using the observed $R$ and the estimated value of the next state-action pair $Q(S', A')$.
    * Update variables for the next iteration: $S \leftarrow S'$ and $A \leftarrow A'$.

---

### **Question 2 & 3: Write and explain off-policy TD control using Q-learning / Describe the Q-learning algorithm for TD control. (10 marks)**

**Answer:**

**1. Concept of Off-Policy TD Control via Q-Learning:**
**Q-LEARNING** is one of the most famous breakthroughs in Reinforcement Learning. It is an **OFF-POLICY** Temporal Difference (TD) control algorithm. 
* **TD Control:** It learns step-by-step (online) and simultaneously evaluates and improves the policy.
* **Off-Policy Nature:** The agent uses an exploratory behavior policy (like $\epsilon$-greedy) to move around the environment. However, when it updates its internal $Q$-table, it **IGNORES** the exploratory action it is about to take. Instead, it aggressively updates its knowledge based on the **ABSOLUTE MAXIMUM** possible $Q$-value of the next state.

**2. The Q-Learning Mathematical Formula:**
$$Q(S_t, A_t) \leftarrow Q(S_t, A_t) + \alpha \left[ R_{t+1} + \gamma \max_a Q(S_{t+1}, a) - Q(S_t, A_t) \right]$$

**Explanation of the Formula Components:**
* $Q(S_t, A_t)$: The current estimated value of taking action $A_t$ in state $S_t$.
* $\alpha$: The LEARNING RATE.
* $R_{t+1}$: The actual immediate reward observed.
* $\gamma$: The DISCOUNT FACTOR.
* **$\max_a Q(S_{t+1}, a)$:** This is the crucial off-policy component. It represents the value of the **GREEDIEST, BEST possible action** in the next state, regardless of what action the agent actually ends up taking.
* The term in the brackets is the **TD Error**.

**3. Step-by-Step Q-Learning Algorithm:**
* **Step 1:** Initialize the action-value function $Q(s, a)$ arbitrarily for all state-action pairs (terminal states = 0).
* **Step 2:** Loop for each episode:
    * Initialize the starting state $S$.
* **Step 3:** Loop for each step of the episode until $S$ is terminal:
    * Choose an action $A$ from state $S$ using a behavior policy derived from $Q$ (e.g., **$\epsilon$-GREEDY** to ensure continuous exploration).
    * Execute action $A$ in the environment. Observe the immediate reward $R$ and the resulting next state $S'$.
    * Update the $Q$-value for $Q(S, A)$ using the formula:
        $$Q(S, A) \leftarrow Q(S, A) + \alpha \left[ R + \gamma \max_a Q(S', a) - Q(S, A) \right]$$

    * Update the current state for the next step: $S \leftarrow S'$. *(Notice we do NOT carry over the action $A'$, unlike in SARSA).*

**4. Why Q-Learning is Powerful (Examiner's Note for Max Marks):**
Because Q-learning directly approximates the optimal action-value function $q^*$, independent of the policy being followed, the convergence proofs are much simpler. It guarantees that the agent will eventually find the exact mathematical optimal policy, provided that all state-action pairs continue to be visited and updated.

