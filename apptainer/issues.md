# Known issues

## GPU Server (on kyutech)

- Please refere this [issue](https://github.com/pytorch/pytorch/issues/107300).

### Error

```bash
Traceback (most recent call last):
  File "/opt/venv/lib/python3.10/site-packages/lerobot/configs/parser.py", line 227, in wrapper_inner
    response = fn(cfg, *args, **kwargs)
  File "/home/yano21/usr/bootup_vla/lerobot/lerobot/scripts/train.py", line 139, in train
    policy = make_policy(
  File "/opt/venv/lib/python3.10/site-packages/lerobot/common/policies/factory.py", line 152, in make_policy
    policy.to(cfg.device)
  File "/opt/venv/lib/python3.10/site-packages/torch/nn/modules/module.py", line 1343, in to
    return self._apply(convert)
  File "/opt/venv/lib/python3.10/site-packages/torch/nn/modules/module.py", line 903, in _apply
    module._apply(fn)
  File "/opt/venv/lib/python3.10/site-packages/torch/nn/modules/module.py", line 903, in _apply
    module._apply(fn)
  File "/opt/venv/lib/python3.10/site-packages/torch/nn/modules/module.py", line 930, in _apply
    param_applied = fn(param)
  File "/opt/venv/lib/python3.10/site-packages/torch/nn/modules/module.py", line 1329, in convert
    return t.to(
  File "/opt/venv/lib/python3.10/site-packages/torch/cuda/__init__.py", line 336, in _lazy_init
    raise DeferredCudaCallError(msg) from e
torch.cuda.DeferredCudaCallError: CUDA call failed lazily at initialization with error: device >= 0 && device < num_gpus INTERNAL ASSERT FAILED at "/pytorch/aten/src/ATen/cuda/CUDAContext.cpp":49, please report a bug to PyTorch. device=1, num_gpus=

CUDA call was originally invoked at:
```

### Solution

- Set Cuda device ID for using

```bash
export CUDA_VISIBLE_DEVICES=1
```

## When Start Training

- Hugging faceからのダウンロードが途中で止まってしまう
    - とりあえずもう一回ダウンロードを開始すればOK


```bash
huggingface_hub.errors.HfHubHTTPError: 429 Client Error: Too Many Requests for url: https://huggingface.co/api/datasets/lerobot/pusht/xet-read-token/6e1d9c95aaf8abb19342e723935b6af7c54b5903
```