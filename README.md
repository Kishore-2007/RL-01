# Representation-of-a-Real-World-Problem-as-a-Markov-Decision-Process

## Date : 27-10-2026

## Aim :

To represent a student’s daily study decision problem as a Markov Decision Process by defining its states, actions, transition probabilities, rewards, discount factor, and a Python representation.
---

## Problem Statement :

### Problem Description
A student has to decide, at each study session, whether to Study or Rest. Studying earns useful progress but drains energy. Resting restores energy but gives little progress. The student’s current energy level (High, Medium or Low) decides what happens next, and the outcome is uncertain: studying doesn’t always drain energy by the same amount. The goal is to choose actions that maximize total long-term benefit.
---

## MDP Components :

A Markov Decision Process is represented as:

$$
MDP = (S, A, P, R, \gamma)
$$

Where:

| Symbol | Meaning |
|---|---|
| $S$ | Set of states |
| $A$ | Set of actions |
| $P$ | Transition probability function |
| $R$ | Reward function |
| $\gamma$ | Discount factor |

---

## State Space

The state is the student’s energy level.

```text
S = { High, Medium, Low }
```

---

## Sample State

s = Medium (the student has moderate energy).

---

## Action Space

Decides that Student has to study or rest.

```text
A = { Study, Rest }
```

---

## Sample Action

a = Study

---
## Transition Probability

The transition probability function **P(s′ | s, a)** gives the probability of reaching the next energy level **s′** after taking action **a** in state **s**.

| Current State (s) | Action (a) | Next State (s′) | Probability P(s′ \| s, a) |
|:---:|:---:|:---:|:---:|
| High | Study | High | 0.4 |
| High | Study | Medium | 0.6 |
| High | Rest | High | 1.0 |
| Medium | Study | Medium | 0.4 |
| Medium | Study | Low | 0.6 |
| Medium | Rest | High | 0.7 |
| Medium | Rest | Medium | 0.3 |
| Low | Study | Low | 1.0 |
| Low | Rest | Medium | 0.8 |
| Low | Rest | Low | 0.2 |

For every state-action pair, the probabilities sum to 1.

**Example:**

```
P(Low | Medium, Study) = 0.6
```

This means that if the student studies while at Medium energy, there is a 60% chance their energy drops to Low.

---

## Reward Function

The reward function **R(s, a, s′)** gives the feedback the student receives after taking action **a** in state **s** and moving to state **s′**. Here the reward depends only on the current state and action, so **R(s, a, s′) = R(s, a)**.

| State (s) | Action (a) | Reward R(s, a) | Reason |
|:---:|:---:|:---:|---|
| High | Study | +10 | Very productive |
| High | Rest | 0 | Wasted energy |
| Medium | Study | +6 | Moderately productive |
| Medium | Rest | +1 | Recovers energy |
| Low | Study | -5 | Tired, so poor learning |
| Low | Rest | +2 | Good recovery |

**Discount Factor:**

```
γ = 0.9
```

**Example:**

```
R(High, Study) = +10
```

---

## Graphical Representation

Each arrow is labelled as **Action, Probability, Reward**.

<img width="772" height="442" alt="image" src="https://github.com/user-attachments/assets/9fcc44a8-e47f-4e08-8ba1-2f81e56945ea" />

---

## Python Representation

```python
# MDP Representation using Python
print("Name: Kishore S")
print("Register Number: 212224230130")

states = ["High", "Medium", "Low"]
actions = ["Study", "Rest"]
gamma = 0.9

# P[state][action] = list of (probability, next_state, reward)
P = {
    "High": {
        "Study": [(0.4, "High", 10), (0.6, "Medium", 10)],
        "Rest":  [(1.0, "High", 0)]
    },
    "Medium": {
        "Study": [(0.4, "Medium", 6), (0.6, "Low", 6)],
        "Rest":  [(0.7, "High", 1), (0.3, "Medium", 1)]
    },
    "Low": {
        "Study": [(1.0, "Low", -5)],
        "Rest":  [(0.8, "Medium", 2), (0.2, "Low", 2)]
    }
}

print("\nStates :", states)
print("Actions:", actions)
print("Gamma  :", gamma)

print("\nTransitions:")
for s in P:
    for a in P[s]:
        total = 0
        for prob, s_next, r in P[s][a]:
            print(f"P({s_next} | {s}, {a}) = {prob}, Reward = {r}")
            total += prob
        assert abs(total - 1.0) < 1e-9, f"Probabilities for ({s},{a}) don't sum to 1"

print("\nAll transition probabilities are valid.")

```
---
## Output

<img width="681" height="397" alt="image" src="https://github.com/user-attachments/assets/b84a631a-7447-42b5-be6f-86590580d7f1" />

---

## Result

The student's daily study decision problem was successfully represented as a Markov Decision Process (MDP).

- **States (S):** High, Medium, Low (student's energy level)
- **Actions (A):** Study, Rest
- **Transition Probability (P):** Defined for every state-action pair, with probabilities summing to 1
- **Reward Function (R):** Positive for productive study and recovery, negative for studying while tired
- **Discount Factor (γ):** 0.9

The MDP was represented using Python dictionaries, and the graphical representation was drawn with states as nodes and actions as arrows labelled with probabilities and rewards. Thus, a real-world sequential decision-making problem was formally modelled as an MDP.

---

