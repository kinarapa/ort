# Train PyTorch models with ONNX Runtime

ONNX Runtime for PyTorch accelerates PyTorch model training using ONNX Runtime.

It is available via the torch-ort python package.

This repository contains the source code for the package as well as instructions for running the package and samples demonstrating how to do so.

## Pre-requisites

You need a machine with at least one NVIDIA or AMD GPU to run ONNX Runtime for PyTorch.

You can install and run torch-ort in your local environment, or with Docker.

## Run in a Python environment

### Default dependencies

By default, torch-ort depends on PyTorch 1.8.1, ONNX Runtime 1.8 and CUDA 10.2.

1. Install CUDA 10.2

2. Install CuDNN 7

3. Install torch-ort and dependencies

    - `pip install onnx ninja`
    - `pip install torch-ort`

### Explicitly install for NVIDIA CUDA 10.2

1. Install CUDA 10.2

2. Install CuDNN 7

3. Install torch-ort and dependencies

    - `pip install onnx ninja`
    - `pip install torch==1.8.1`
    - `pip install --pre onnxruntime-training -f https://onnxruntimepackages.z14.web.core.windows.net/onnxruntime_nightly_cu102.html`
    - `pip install torch-ort`

### Explicitly install for NVIDIA CUDA 11.1

1. Install CUDA 11.1

2. Install CuDNN 8

3. Install torch-ort and dependencies

    - `pip install onnx ninja`
    - `pip install torch==1.8.1`
    - `pip install --pre onnxruntime-training -f https://onnxruntimepackages.z14.web.core.windows.net/onnxruntime_nightly_cu111.html`
    - `pip install torch-ort`

### Explicitly install for AMD ROCm 4.1

1. Install ROCm 4.1 base package ([instructions](https://rocmdocs.amd.com/en/latest/Installation_Guide/Installation-Guide.html))

2. Install ROCm 4.1 libraries ([instructions](https://rocmdocs.amd.com/en/latest/Installation_Guide/Software-Stack-for-AMD-GPU.html#machine-learning-and-high-performance-computing-software-stack-for-amd-gpu-v4-1))

3. Install ROCm 4.1 RCCL ([instructions](https://github.com/ROCmSoftwarePlatform/rccl/tree/rocm-4.1.0))

4. Install torch-ort and dependencies
    - `pip install onnx ninja`
    - `pip install --pre torch -f https://download.pytorch.org/whl/nightly/rocm4.1/torch_nightly.html`
    - `pip install --pre onnxruntime-training -f https://onnxruntimepackages.z14.web.core.windows.net/onnxruntime_nightly_rocm41.html`
    - `pip install torch-ort`

## Run using Docker

The [docker](docker) directory contains dockerfiles for NVIDIA CUDA 10.2 and NVIDIA CUDA 11.1 configurations.

- [docker/ort-cu102-cudnn7-devel-ubuntu18.04-dockerfile](docker/ort-cu102-cudnn7-devel-ubuntu18.04-dockerfile)
- [docker/ort-cu111-cudnn8-devel-ubuntu18.04-dockerfile](docker/ort-cu111-cudnn8-devel-ubuntu18.04-dockerfile)

1. Build the docker image

    `docker build -t torch-ort:latest -f docker/ort-cu102-cudnn7-devel-ubuntu18.04-dockerfile .`

2. Run the docker container using the image you have just built

    `docker run -it --gpus all torch-ort:latest`

## Test your installation

1. Clone this repo

- `git clone git@github.com:pytorch/ort.git`

2. Install extra dependencies

- `pip install wget pandas sklearn transformers`

3. Run the training script

- `python ./ort/tests/bert_for_sequence_classification.py`

## Add ONNX Runtime for PyTorch to your PyTorch training script

```python
import onnxruntime
from torch_ort import ORTModule
model = ORTModule(model)
# PyTorch training script follows
```

