---
title: Windows10에서 tesorflow-gpu 사용하기 (How to use tensorflow-gpu in Windows10)
categories:
  - Tensorflow
tags:
  - Tensorflow-gpu
  - Windows 10
---

>### Requirements

- Python > 3.5
- Nvidia CUDA GPU. (사용하고 있는 GPU가 CUDA 호환인지는 [여기](https://developer.nvidia.com/cuda-gpus)에서 확인 가능)


>### 1. Nvidia GPU 라이브러리 Setting

- Cuda Toolkit 8.0 과 cuDNN v5.1 설치

## (1) Download & install CUDA Toolkit  
- Toolkit version 8.0 or above: https://developer.nvidia.com/cuda-downloads
- Installation directory: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0

## (2) Download and install cuDNN
- cuDNN version 5.1 library for Windows 10: https://developer.nvidia.com/cudnn
- 다운로드를 위해선 Nvidia에 회원 가입이 필요하며,  cuDNN 파일들을 압축해제하여 다음과 같이 Toolkit directory에 복사.

 cuDNN files

Environmental variables
Ensure after installing CUDA toolkit, the CUDA_HOME is set in the environmental variables. If not then you need to add it manually..

 cuDNN files

And path variables as..

 cuDNN files

Install Anaconda
We will install Anaconda as it helps us to easily manage separate environments for specific distributions of Python, without disturbing the version of python installed on your system.

Download and install
Anaconda

Create conda environment
Create new environment, with the name tensorflow-gpu and python version 3.5.2
conda create -n tensorflow-gpu python=3.5.2

 conda

Activate the environment activate tensorflow-gpu

 conda

Install tensorFlow
pip install tensorflow-gpu

 conda

Done. You have successfully installed TensorFlow with GPU on your Windows machine.
Now lets test if it is using GPU…

Activate environment we created
activate tensorflow-gpu

Test GPU
Enter into python shell
python

import tensorflow as tf

Now run this command and check if it identifies your GPU.
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))

 tf
