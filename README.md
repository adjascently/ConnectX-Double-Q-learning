# ConnectX AI Agent using Double Q-Learning

ConnectX is a generalized version of the classic Connect Four game, where players aim to align a specific number of their pieces consecutively in a grid—either horizontally, vertically, or diagonally. This project implements a **Double Q-Learning** (DQL) approach to train an AI agent that learns to play ConnectX effectively through self-play and reinforcement learning.

---

## 🧠 Problem Formulation

- **States**: The current configuration of the game board.
- **Actions**: The columns in which a piece can be dropped.
- **Rewards**:
  - `+1` for a winning move
  - `-1` for a losing move
  - `0` for all intermediate moves
- **Transitions**: The next state is influenced by the opponent’s move, making the environment partially stochastic.

---

## 🎯 Reward Function

- `+1` → Winning move  
- `-1` → Losing move  
- `0` → Non-terminal or intermediate move  

---

## 🏋️ Training Process

- The agent learns by **self-play** to discover optimal strategies.
- Training is conducted over **N episodes** using a **decaying epsilon** for exploration.
- **Q-values** are updated based on the outcomes of episodes.
- After training, the agent uses the learned **Q-tables** to infer the best actions during test gameplay.

---

## 🔄 Double Q-Learning Overview

Double Q-Learning is an improvement over standard Q-learning that **reduces overestimation bias** by maintaining two independent Q-tables:

- **Q1** and **Q2** tables are initialized separately.
- The agent chooses actions using an **epsilon-greedy policy** based on the sum of Q1 and Q2.
- Updates alternate between Q1 and Q2:
  - With probability 0.5, update Q1 using the best action from Q2.
  - Otherwise, update Q2 using the best action from Q1.

This alternating update strategy helps stabilize learning and improves generalization.

---

## 📌 Algorithm Steps

1. **Initialize** Q1 and Q2 tables with zeros.
2. **For each episode**:
   - Use **epsilon-greedy** policy to select an action based on Q1 + Q2.
   - Execute the action, observe reward and next state.
   - With 50% probability:
     - **Update Q1** using Q2’s action selection.
     - Otherwise, **update Q2** using Q1’s action selection.
3. Repeat for a predefined number of episodes or until convergence.

---


