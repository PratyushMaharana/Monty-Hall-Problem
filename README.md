# Monty Hall Problem
The Monty Hall Problem is a classic probability puzzle based on a game show scenario. A contestant picks one of three doors, behind one is a prize (like a car) and behind the others are goats. After the choice, the host (who knows what’s behind each door) opens a different door to reveal a goat. The contestant then decides to either stay with the original door or switch to the remaining unopened door. Counterintuitively, switching doors doubles the chance of winning (about 2/3) compared to staying with the initial choice (about 1/3). This repository contains a Python Jupyter Notebook that simulates the Monty Hall game to verify these success rates.
# How to Run
Clone or download the repo: Get the notebook file monty_hall_problem.ipynb to your local machine.
Install Python 3: Ensure you have Python 3.x installed. You can use a virtual environment if you like.
Optional libraries: The basic simulation uses only Python’s standard random and timeit modules. The notebook also shows a NumPy-based approach (which requires NumPy). You can install NumPy with pip install numpy if you want to run that part. (No other external libraries are needed.)
Open the notebook: Launch Jupyter Notebook or JupyterLab and open monty_hall_problem.ipynb.
Run the cells: Execute the cells in order. The notebook will run simulations of the game and print the success rates for switching vs. staying.
# Code Highlights
Simulation loop (pure Python): The core simulation runs many trials by randomly placing the prize, making a first choice, having the host remove a goat, and recording wins for switching vs. staying. For example:
for _ in range(repeats):
    doors = [0,0,0]
    doors[random.randint(0,2)] = 1
    first_choice = doors.pop(random.randint(0,2))
    if doors[0] == 0:
        doors.pop(0)
    else:
        doors.pop(1)
    keep_results.append(first_choice)
    switch_results.append(doors[0])
(From the notebook​
github.com
​
github.com
.)
NumPy vectorized approach: The notebook also demonstrates a compact simulation using NumPy arrays. It assigns the prize and choices across a large array and computes means. For example:
import numpy as np
repeats = 1_000_000
doors = np.zeros((repeats,3))
doors[:,0] = 1
rng = np.random.default_rng()
rng.permuted(doors, axis=1, out=doors)
doors[:, 1:].sort()
means = doors.mean(axis=0)
print(f"switching win rate: {means[2]:.3%}")
print(f"staying win rate:  {means[0]:.3%}")
(From the notebook​
github.com
​
github.com
.)
Results
Running the simulations confirms the expected probabilities. In the notebook’s output, the success rate for switching doors is about 66.7%, while staying yields about 33.3%​
github.com
. This matches the theoretical result that switching doubles the chance of winning. For example, one run showed “the success rate when switching is 66.663%” and “when keeping is 33.337%”​
github.com
.
License
This project is released under the MIT License. Feel free to use and modify the code as needed.
