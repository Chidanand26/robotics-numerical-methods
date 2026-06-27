# Robotics Numerical Methods

> Numerical linear algebra and robot-arm kinematics in Python.

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?logo=python&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

## Overview

A small collection of Python scripts applying numerical linear algebra to
engineering and robotics problems. It pairs classic solver routines
(Gaussian elimination, LU decomposition, matrix rank) with statics problems
(spring networks, trusses) and forward-kinematics models of 2R and 3R planar
robot arms. Each script is self-contained and runnable on its own.

The code originated as a 3rd-semester Linear Algebra lab set and has been
reorganized into a tidy, portfolio-ready structure.

## Features / Scripts

| Script | What it computes | Key concept |
| --- | --- | --- |
| `src/robot_3R_arm.py` | Workspace, configuration space (C-space) and 2x3 Jacobian (with its null space) of a 3-link planar arm | Robot arm forward kinematics, Jacobian / null space |
| `src/robot_2R_arm.py` | Reachable workspace and a sample configuration of a 2-link planar arm | Robot arm forward kinematics |
| `src/gauss_elimination.py` | Solves a linear system by Gaussian elimination with back substitution; also demonstrates an LU solver | Gaussian elimination |
| `src/lu_decomposition.py` | Factors A into L and U and solves Ax = b via Ly = b, Ux = y | LU decomposition |
| `src/augmented_matrix.py` | Row-reduces an augmented matrix `[A \| b]` and back-substitutes for the solution | Gaussian elimination |
| `src/spring_system.py` | Builds a spring stiffness matrix and solves for nodal displacements | Spring statics (linear system) |
| `src/truss_analysis.py` | Solves joint-equilibrium equations for truss member forces | Truss statics (linear system) |
| `src/matrix_rank.py` | Computes the rank of a matrix of stacked vectors (dimension of their span) | Matrix rank / span |

## Robotics Highlight

The robot-arm scripts implement **forward kinematics of planar revolute arms**.
For a link of length `L` at cumulative joint angle `phi`, each segment
contributes `(L*cos(phi), L*sin(phi))` to the end-effector position, summed
along the chain:

- **2R arm** (`robot_2R_arm.py`): two links `L1, L2`. The end-effector is
  `x = L1*cos(t1) + L2*cos(t1+t2)`, `y = L1*sin(t1) + L2*sin(t1+t2)`. Sweeping
  the joint angles traces the reachable workspace; a sample `(t1, t2)` pose is
  drawn over it.
- **3R arm** (`robot_3R_arm.py`): three links `L1, L2, L3`, extending the same
  summation with a third term. Beyond the 2D workspace it visualizes the 3D
  configuration space and builds the **2x3 Jacobian** at a sample pose. Its
  **null space** (computed with `scipy.linalg.null_space`) gives the joint
  velocity directions that produce no end-effector motion — a glimpse of arm
  redundancy.

## Tech Stack

- Python 3
- [NumPy](https://numpy.org/) — array math and linear-algebra solvers
- [Matplotlib](https://matplotlib.org/) — workspace and C-space plots
- [SciPy](https://scipy.org/) — `scipy.linalg.null_space` for the Jacobian analysis

## Project Structure

```
.
├── src/
│   ├── robot_3R_arm.py        # 3R arm FK, C-space, Jacobian null space
│   ├── robot_2R_arm.py        # 2R arm FK + workspace
│   ├── gauss_elimination.py   # Gaussian elimination (+ LU demo)
│   ├── lu_decomposition.py    # LU decomposition solver
│   ├── augmented_matrix.py    # Augmented-matrix row reduction
│   ├── spring_system.py       # Spring stiffness system
│   ├── truss_analysis.py      # Truss equilibrium
│   └── matrix_rank.py         # Matrix rank / span dimension
├── docs/
│   ├── index.html             # Original coursework write-up page
│   └── images/                # Lab screenshots (problems, code, outputs)
├── requirements.txt
├── LICENSE
└── README.md
```

## Installation

```bash
pip install -r requirements.txt
```

## Usage

Run any script directly, for example:

```bash
python src/robot_3R_arm.py    # opens plots, prints Jacobian null space
python src/robot_2R_arm.py    # opens the 2R workspace plot
python src/gauss_elimination.py
python src/matrix_rank.py
```

Scripts that build plots open Matplotlib windows; the linear-algebra solvers
print their results to the console.

## Results / Outputs

Screenshots captured from the original lab sessions live in `docs/images/`.
They are grouped by lab, with `q` denoting the problem statement, `c` the code,
and `a` the program output:

- `lab1q/lab1c/lab1a.png` — spring-system displacement solution.
- `lab2q/lab2c/truss.jpeg` — truss member-force analysis.
- `lab3aq/lab3ac/lab3aa.png` and `lab3bq/lab3bc/lab3ba.png`, `gauss.jpeg` —
  Gaussian elimination / linear-system solutions.
- `lab4q/lab4c/lab4a.png`, `lab4r.png` — LU decomposition results.

(The screenshots show the actual console outputs and plots produced by the
scripts; see the images for the specific numbers.)

## Future Improvements

- Add **inverse kinematics** for the 2R and 3R arms.
- Use the existing **Jacobian** for velocity control and singularity detection.
- **Animate** arm motion through a joint trajectory.
- Refactor solvers into a shared, importable module with unit tests.
- Add input validation and pivoting for numerical robustness.

## License

This project is licensed under the [MIT License](LICENSE).

## Author

**Chidanand S Karennavar**
GitHub: [@Chidanand26](https://github.com/Chidanand26)

## Contributing

Contributions and suggestions are welcome. Feel free to open an issue or submit
a pull request.
