# Apptainer(Singularity) for LeRobot

## How to build

```bash
cd lerobot/apptainer
apptainer build --fakeroot --sandbox your_path/lerobot_sandbox lerobot_cuda122.def
```

## How to run

```bash
apptainer shell --nv --bind /run/user/1000 --bind /var/lib/dbus/machine-id your_path/lerobot_sandbox 
source /entrypoint.sh
```

## How to modify

```bash
apptainer shell --fakeroot --writable your_path/lerobot_sandbox lerobot_cuda122.def
```

## (TODO): Initalize process

### python packages

```bash
cd lerobot/
pip install .
pip install ".[aloha, pusht, xarm]"
```

### (Optional) login to wandb

- Copy your API key in [Wandb](https://wandb.ai/settings#api).

```bash
wandb login
```
