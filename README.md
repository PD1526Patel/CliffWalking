This repository implements two classic Temporal Difference (TD) control algorithms—**SARSA** (On-Policy) and **Q-Learning** (Off-Policy)—to solve the standard **Cliff Walking** gridworld environment from Gymnasium (originally OpenAI Gym).

---

## 🎮 The Environment

The Cliff Walking environment is a 4x12 gridworld where the agent starts at the bottom-left corner and must reach the goal at the bottom-right corner.

<div align="center">
  <img src="assets/SARSA.png" width="700" alt="Cliff Walking Gridworld"/>
</div>

### Grid Layout:

- **Start (S):** Bottom-left tile `[3, 0]` (State 36).
- **Goal (G):** Bottom-right tile `[3, 11]` (State 47).
- **Cliff (C):** The tiles between the start and goal `[3, 1..10]` (States 37 to 46).
- **Step Penalty:** Every step incurs a reward of `-1`.
- **Cliff Penalty:** Stepping onto the cliff sends the agent back to the **Start** and incurs a penalty of `-100`.

---

## 🧠 Algorithms Implemented

### 1. Q-Learning (Off-Policy TD Control)

Q-Learning learns the optimal action-value function ($Q^*$) directly, assuming the agent follows a greedy policy, regardless of the exploratory actions taken.

- **Update Rule:**
  $$Q(s, a) \leftarrow Q(s, a) + \alpha \left[ r + \gamma \max_{a'} Q(s', a') - Q(s, a) \right]$$
- **Behavior:** Because it assumes optimal actions in the next state, Q-Learning learns the optimal path that runs **directly along the edge of the cliff**. During training/exploration, this makes it fall into the cliff frequently.

### 2. SARSA (On-Policy TD Control)

SARSA updates its action-value function based on the actual action ($a'$) taken by the current policy (e.g., $\epsilon$-greedy), accounting for exploration.

- **Update Rule:**
  $$Q(s, a) \leftarrow Q(s, a) + \alpha \left[ r + \gamma Q(s', a') - Q(s, a) \right]$$
- **Behavior:** Because it anticipates the possibility of exploratory random moves (which could plunge it off the cliff), SARSA learns a **safer, longer path** that stays far away from the cliff edge.

---

## 📁 Repository Structure

```text
├── assets/
│   └── SARSA.png    # Environment visualization
│   └── Q_Learning.png    # Environment visualization
├── Q_Learning.ipynb            # Jupyter notebook for Q-Learning implementation
├── SARSA.ipynb                 # Jupyter notebook for SARSA implementation
├── generate_env_image.py       # Script to generate Gymnasium rendering
├── README.md                   # Project documentation (this file)
└── .gitignore                  # Git ignored files
```

---

## 🛠️ Installation & Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/PD1526Patel/CliffWalking.git
   cd CliffWalking
   ```

2. **Install the dependencies:**
   Make sure you have Python 3.8+ installed, then install the required libraries:

   ```bash
   pip install gymnasium pygame numpy matplotlib jupyter
   ```

3. **Run the Notebooks:**
   Launch Jupyter Notebook or open the project in VS Code:
   ```bash
   jupyter notebook
   ```
   Explore the implementation details and training results in [Q_Learning.ipynb](Q_Learning.ipynb) and [SARSA.ipynb](SARSA.ipynb).
