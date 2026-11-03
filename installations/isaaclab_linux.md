# Isaac Lab on Linux

This project uses Isaac Lab 3.0.

The releases of Isaac Lab are listed here: https://github.com/isaac-sim/IsaacLab/releases

Install uv (it manages Python and the dependencies), then open a new terminal:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Clone Isaac Lab:

```bash
git clone https://github.com/isaac-sim/IsaacLab.git --branch main
```

Enter the folder:

```bash
cd IsaacLab
```

Training on CPU with the Newton physics engine, without Isaac Sim (3 iterations of a test task). The first run downloads and installs the dependencies, so it takes a while:

```bash
uv run isaaclab train --rl_library rsl_rl --task Isaac-Cartpole --device cpu --num_envs 64 --max_iterations 3 physics=newton_mjwarp
```

Training on an NVIDIA GPU with the Newton physics engine:

```bash
uv run isaaclab train --rl_library rsl_rl --task Isaac-Cartpole-Direct physics=newton_mjwarp
```

Training with Isaac Sim, which needs a supported RTX GPU and 32 GB of RAM. At the first run, accept the NVIDIA license:

```bash
uv run --extra all --extra isaacsim --extra video isaaclab train --rl_library rsl_rl --task Isaac-Cartpole-Direct physics=isaacsim_physx
```

The results are saved in `logs/rsl_rl/<experiment-name>/<date-and-time>/`.

More about Isaac Sim, the play of a trained model and the videos: [IsaacLab.md](IsaacLab.md)
