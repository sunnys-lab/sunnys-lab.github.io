#Requirements
Python > 3.5
Nvidia CUDA GPU. You can check here if your GPU is CUDA compatible.

#Setting up your Nvidia GPU
You need to install Cuda Toolkit 8.0 and cuDNN v5.1 as the GPU version works best with these.

##Download and install CUDA Toolkit
Toolkit version 8.0 or above: https://developer.nvidia.com/cuda-downloads
Example installation directory: C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0

##Download and install cuDNN
cuDNN version 5.1 library for Windows 10: https://developer.nvidia.com/cudnn
You would need to signup at Nvidia in order to download these files. Now extract the cuDNN files into your Toolkit directory.

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
