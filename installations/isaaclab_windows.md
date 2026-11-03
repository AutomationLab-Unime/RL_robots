# Isaac Lab on Windows

Windows 11 is supported by Isaac Lab 3.0.

The releases of Isaac Lab are listed here: https://github.com/isaac-sim/IsaacLab/releases

Open PowerShell **as administrator** and enable the long paths (only once):

```powershell
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" -Name "LongPathsEnabled" -Value 1 -PropertyType DWORD -Force
```

Open a new **Command Prompt** (not PowerShell) and install uv:

```bat
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Close the Command Prompt and open a new one. Clone Isaac Lab (it needs [Git for Windows](https://git-scm.com)):

```bat
git clone https://github.com/isaac-sim/IsaacLab.git --branch main
```

Enter the folder:

```bat
cd IsaacLab
```

Training on CPU with the Newton physics engine, without Isaac Sim (3 iterations of a test task). The first run downloads and installs the dependencies, so it takes a while:

```bat
uv run isaaclab train --rl_library rsl_rl --task Isaac-Cartpole --device cpu --num_envs 64 --max_iterations 3 physics=newton_mjwarp
```

With an NVIDIA GPU (driver 595.97 or newer) remove `--device cpu`. The Isaac Sim extra (`--extra isaacsim`) needs a supported RTX GPU and 32 GB of RAM.

Play the trained model (it loads the last checkpoint). The `viser` extra, the viewer that runs in the browser, is downloaded the first time:

```bat
uv run --extra viser isaaclab play --rl_library rsl_rl --task Isaac-Cartpole --device cpu --num_envs 1 physics=newton_mjwarp --viz viser
```

No window opens: open in the browser the address printed in the terminal (by default `http://localhost:8080`). Press `Ctrl+C` in the terminal to stop.
