# mjlab on Windows

The releases of mjlab are listed here: https://github.com/mujocolab/mjlab/releases

Install [Git for Windows](https://git-scm.com), then install uv from PowerShell and open a new terminal:

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Clone mjlab in a folder with a short path (long paths cause problems on Windows):

```powershell
cd C:\
```

```powershell
git clone https://github.com/mujocolab/mjlab.git
```

Enter the folder:

```powershell
cd mjlab
```

Install the dependencies (uv downloads Python too):

```powershell
uv sync
```

Training on CPU of a test task (3 iterations). First hide the GPU from the program, then start the training:

```powershell
$env:CUDA_VISIBLE_DEVICES = ""
```

```powershell
uv run train Mjlab-Cartpole-Balance --gpu-ids None --env.scene.num-envs 16 --agent.max-iterations 3 --agent.logger tensorboard
```

The first start is slower, because the kernels are compiled. Warp prints a warning that it does not find the CUDA driver: it is normal.

`--agent.logger tensorboard` is needed: otherwise mjlab asks for a Weights & Biases account.

Training on GPU on Windows is not covered by the mjlab documentation (it asks for Linux).

The results are saved in `logs\rsl_rl\cartpole\<date-and-time>\`. The training curves can be visualized with:

```powershell
uv run tensorboard --logdir logs/rsl_rl --port 6006
```
