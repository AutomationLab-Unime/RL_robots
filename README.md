# RL_robots

Reinforcement learning for robot motion control: guides to install the simulators, and one branch for each project.

## Simulators

The [installations](installations) folder contains the guides to install the simulators on the different operating systems:

- Isaac Lab: [Linux](installations/isaaclab_linux.md), [Windows](installations/isaaclab_windows.md), [macOS](installations/isaaclab_macos.md)
- Mujoco Lab: [Linux](installations/mjlab_linux.md), [Windows](installations/mjlab_windows.md), [macOS](installations/mjlab_macos.md)

## Projects

Each project is in its own branch:

- [`gait-score-bo`](https://github.com/GabrieleRinaldi/RL_robots/tree/gait-score-bo): locomotion policy for the Unitree B1 quadruped, with the reward weights optimized by Bayesian Optimization (Isaac Lab 3.0)
