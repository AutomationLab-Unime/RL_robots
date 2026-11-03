# mjlab on macOS

Works on Macs with Apple Silicon (M1 or newer). Macs with an Intel processor are not supported.

The releases of mjlab are listed here: https://github.com/mujocolab/mjlab/releases

Install the Apple command line tools (they contain Git), if you do not have them:

```bash
xcode-select --install
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

The mjlab documentation says that on macOS only the evaluation of trained models is supported: the training on CPU works, but it is only for tests. A real training needs Linux and an NVIDIA GPU.

The results are saved in `logs/rsl_rl/cartpole/<date-and-time>/`. The training curves can be visualized with:

```bash
uv run tensorboard --logdir logs/rsl_rl --port 6006
```
