# Isaac Lab on macOS (Docker)

Isaac Lab cannot be installed natively on macOS. On a Mac with Apple Silicon it runs in a Linux container (ARM), without Isaac Sim. The container has no GPU, so the training is only on CPU.

The releases of Isaac Lab are listed here: https://github.com/isaac-sim/IsaacLab/releases

Install [Docker Desktop for Mac with Apple chip](https://www.docker.com/products/docker-desktop/) and open it. In Settings > Resources give it enough memory (we suggest at least 8 GB).

Download the Isaac Lab image (5.3 GB, version 3.0.0 without Isaac Sim):

```bash
docker pull nvcr.io/nvidia/isaac-lab:3.0.0-kitless
```

Training on CPU of a test task (5 iterations):

```bash
docker run --rm nvcr.io/nvidia/isaac-lab:3.0.0-kitless isaaclab train --rl_library rsl_rl --task Isaac-Cartpole-Direct --num_envs 16 --device cpu presets=newton_mjwarp agent.device=cpu --max_iterations 5
```

`agent.device=cpu` is needed: in version 3.0.0 without it the training looks for an NVIDIA driver and stops.

To keep the results, start a container that stays active (without the GPU options):

```bash
docker run --name isaac-lab-kitless --detach --interactive --tty -v isaac-lab-kitless-logs:/workspace/isaaclab/logs nvcr.io/nvidia/isaac-lab:3.0.0-kitless
```

Start the training inside the container:

```bash
docker exec isaac-lab-kitless isaaclab train --rl_library rsl_rl --task Isaac-Cartpole-Direct --num_envs 16 --device cpu presets=newton_mjwarp agent.device=cpu --max_iterations 5
```

Copy the results on the Mac:

```bash
docker cp isaac-lab-kitless:/workspace/isaaclab/logs ./logs
```

Stop and remove the container:

```bash
docker stop isaac-lab-kitless
docker rm isaac-lab-kitless
```
