# Monty Hall Problem

The Monty Hall Problem is a classic probability puzzle based on a game show scenario.  
A contestant picks one of three doors — behind one is a prize, and behind the others are goats.  
After the choice, the host, who knows the contents, reveals a goat behind a different door.  
The contestant is then given a choice to stay with their original door or switch to the other unopened door.

Statistically, **switching doors gives a higher chance of winning (about 66.7%)**, while staying gives about **33.3%!**

---

## File Description

- **`monty_hall_problem.ipynb`** : A Jupyter notebook simulating the Monty Hall game 

---

## Prepare Environment

```bash
# (Optional) Create a virtual environment
python3 -m venv monty_env
source monty_env/bin/activate

# Install Jupyter if you don't have it
pip install notebook
```

---

## Run

```bash
# Open the notebook
jupyter notebook monty_hall_problem.ipynb
```

Then run all the cells to simulate 

---

## Code Highlight

here is the code glimpse

```python
for _ in range(repeats):
    doors = [0, 0, 0]
    doors[random.randint(0,2)] = 1
    first_choice = doors.pop(random.randint(0,2))
    if doors[0] == 0:
        doors.pop(0)
    else:
        doors.pop(1)
    keep_results.append(first_choice)
    switch_results.append(doors[0])
```

a faster NumPy version:

```python
import numpy as np
repeats = 1_000_000
doors = np.zeros((repeats, 3))
doors[:,0] = 1
rng = np.random.default_rng()
rng.permuted(doors, axis=1, out=doors)
doors[:, 1:].sort()
means = doors.mean(axis=0)
print(f"switching win rate: {means[2]:.3%}")
print(f"staying win rate:  {means[0]:.3%}")
```

---

## Results

| Strategy  | Winning Probability |
|-----------|----------------------|
| Stay      | ~33.3%               |
| Switch    | ~66.7%               |

Switching is clearly the better strategy!

---


