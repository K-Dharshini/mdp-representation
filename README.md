# MDP REPRESENTATION

## AIM:
To model the **Autonomous Space Rover** problem as a Markov Decision Process (MDP) and demonstrate it with a Python representation.

## PROBLEM STATEMENT:
A planetary rover must travel from its **Base** to target sites to collect samples and then return to the base.   
The environment consists of **Plain**, **Rocky**, and **Hazardous** terrains, which affect rover movement.  
The rover has a **limited battery (High/Low)** and can perform actions such as moving, scanning to reduce uncertainty, collecting samples, and returning to base.  
The objective is to **maximize collected science value while avoiding hazards and conserving energy**.

## State Space:
- Cell types:  
  - `0`: Hazard  
  - `1`: Base  
  - `2`: Plain  
  - `3`: Rocky  
  - `4`: Target  

- Battery levels:  
  - `H`: High  
  - `L`: Low  

Each state is represented as `(Cell, Battery)`.

## Sample State:
(2, H)  
This means the rover is in a Plain cell with High battery.

## Action Space:
The rover can perform the following actions:  
- `0` = Move Left  
- `1` = Move Right  
- `2` = Scan  
- `3` = Collect  
- `4` = Return  

## Sample Action:
4 = Return  
This indicates the rover chooses to return to its base.

## Reward Function:
- `+50` → Successful collection at a target  
- `+100` → Returning to base after collecting a sample  
- `-50` → Entering a hazardous cell  
- `-1` → Each step taken  
- `-2` → Performing a Scan  
- `-5` → Moving when battery = Low  

## Graphical Representation:
<img width="964" height="669" alt="image" src="https://github.com/user-attachments/assets/d26390bf-c8a3-479c-a17a-88ad397f9b3e" />


## PYTHON REPRESENTATION:
```python
import random

# Define states
cells = {0: "Hazard", 1: "Base", 2: "Plain", 3: "Rocky", 4: "Target"}
battery = ["H", "L"]

# State space
states = [(c, b) for c in cells.keys() for b in battery]

# Actions
actions = {0: "Left", 1: "Right", 2: "Scan", 3: "Collect", 4: "Return"}

# Reward function
def get_reward(state, action):
    cell, bat = state
    if cell == 0:
        return -50
    if action == 3 and cell == 4:
        return 50
    if action == 4 and cell == 1:
        return 100
    if action == 2:
        return -2
    if action in [0, 1] and bat == "L":
        return -5
    return -1

# Example simulation
state = (1, "H")  # Base with High battery
print("Initial State:", state)

for step in range(5):
    action = random.choice(list(actions.keys()))
    reward = get_reward(state, action)
    print(f"Action: {actions[action]}, Reward: {reward}")
```

## OUTPUT:
<img width="282" height="144" alt="image" src="https://github.com/user-attachments/assets/f0bd51ce-91b7-4244-8437-fab3cd0ffd1e" />

## RESULT:
The **Autonomous Rover** problem was successfully represented as a Markov Decision Process (MDP). The state space, action space, rewards, and transitions were clearly defined. The Python simulation demonstrates how the rover interacts with its environment and lays the groundwork for reinforcement learning methods to optimize its policy.
