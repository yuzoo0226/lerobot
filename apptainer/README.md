# Apptainer(Singularity) for LeRobot

## How to build

```bash
cd lerobot/apptainer
apptainer build --fakeroot --sandbox your_path/lerobot_sandbox lerobot_cuda124.def
```

## How to run

```bash
apptainer shell --nv --bind /run/user/1000 --bind /var/lib/dbus/machine-id your_path/lerobot_cu124_sandbox 
source /entrypoint.sh
```

## How to modify

```bash
apptainer shell --fakeroot --writable your_path/lerobot_sandbox lerobot_cuda124.def
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

## Commands

```bash
# Eval
python lerobot/scripts/eval.py --policy.path=lerobot/diffusion_pusht --env.type=pusht --eval.batch_size=10 --eval.n_episodes=10 --policy.use_amp=false --policy.device=cuda

# Train
python lerobot/scripts/train.py --output_dir=outputs/train/diffusion_pusht --policy.type=diffusion --dataset.repo_id=lerobot/pusht --seed=100000 --env.type=pusht --batch_size=64 --steps=200000 --eval_freq=25000 --save_freq=25000 --wandb.enable=true
```
