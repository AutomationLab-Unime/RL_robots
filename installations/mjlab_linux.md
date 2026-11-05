# mjlab on Linux

The releases of mjlab are listed here: https://github.com/mujocolab/mjlab/releases

Install Git (skip this step if `git --version` already works). On Debian and Ubuntu:

```bash
sudo apt update
```

```bash
sudo apt install git
```

On Fedora:

```bash
sudo dnf install git
```

Install uv (it manages Python and the dependencies), then open a new terminal:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Clone mjlab:

```bash
git clone https://github.com/mujocolab/mjlab.git
```

Enter the folder:

```bash
cd mjlab
```

Install the dependencies (uv downloads Python too):

```bash
uv sync
```

Training on CPU of a test task (3 iterations):

```bash
CUDA_VISIBLE_DEVICES="" uv run train Mjlab-Cartpole-Balance --gpu-ids None --env.scene.num-envs 16 --agent.max-iterations 3 --agent.logger tensorboard
```

`--agent.logger tensorboard` is needed: otherwise mjlab asks for a Weights & Biases account.

Training on GPU needs an NVIDIA GPU (driver 580 or newer):

```bash
uv run train Mjlab-Cartpole-Balance --agent.logger tensorboard
```

The results are saved in `logs/rsl_rl/cartpole/<date-and-time>/`. The training curves can be visualized with:

```bash
uv run tensorboard --logdir logs/rsl_rl --port 6006
```

The list of the available tasks:

```bash
uv run list-envs
```
