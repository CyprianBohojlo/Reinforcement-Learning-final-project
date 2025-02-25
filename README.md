# Laser Hockey Reinforcement Learning Project   
The final project about the development of a Reinforcement Learning agent for a laser hockey game in the course Reinforcement Learning WiSe 24/25 at the University of Tübingen, Germany.
## Install   
The base environment can be installed using 
```
python3 -m pip install git+https://github.com/martius-lab/hockey-env.git

or add the following line to your pip file

hockey = {editable = true, git = "https://git@github.com/martius-lab/hockey-env.git"}
```
Additionally, we would recommend you to install   
```
pip install swig # when an error occurs while installing box2d-py
pip install torch
```

```
# Setup
# Linter and Formatter
pip install ruff
pip install pre-commit
```

## Algorithms

This project implements the **Soft Actor-Critic (SAC)** algorithm to train an agent to play a laser hockey game. SAC is an off-policy reinforcement learning algorithm that optimizes for both reward maximization and entropy, encouraging exploration.

The key components of the SAC implementation in this project include:

- **Environment Wrapper (`environment.py`)**  
  A wrapper around the `hockey-env` environment that manages state observations, action constraints, and reward shaping.

- **Neural Networks (`networks.py`)**  
  - **Actor Network**: Learns a policy to output actions based on states.
  - **Critic Networks**: Two critics are used to estimate Q-values and mitigate overestimation bias.
  - **Value Network**: Estimates the expected return from a given state.

- **Replay Buffer (`replay.py`)**  
  A memory buffer storing past experiences to enable batch updates and break correlation in training data.

- **SAC Agent (`sac.py`)**  
  Implements the Soft Actor-Critic agent, including:
  - Policy learning with reparameterization trick.
  - Twin Q-learning for stability.
  - Adaptive entropy tuning to balance exploration and exploitation.

- **Training Pipeline (`train.py`)**  
  - Implements training loops, logging, evaluation, and model saving.
  - Uses an **adaptive learning rate controller** to fine-tune learning dynamically.

- **Training Execution (`training_sac_agent.py`)**  
  - Provides command-line arguments for training and evaluation.
  - Supports multiple training modes (normal, shooting, defense, opponent modes).
  - Handles model saving, resuming training, and performance evaluation.

## Usage

To train the SAC agent, run:

```bash
python training_sac_agent.py --mode normal --max_episodes 1000 --device cpu
