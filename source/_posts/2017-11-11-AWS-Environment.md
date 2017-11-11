---
title: 在AWS 2017年11月版的Spot Instance(競價實例)中建構tensorflow/keras環境 
date: 2017-11-11 01:03:10
tags:
	- AWS
	- Environment Setting
	- Tensorflow
	- Keras
	- Ubuntu 16.04
---


# AWS Spot Instance Compare

Target capacity : 1 instance
AMI : Ubuntu 16.04 LTS
Allocation strategy : Lowest price
EBS volumes : 30 GB
Security groups : default
keras : 2.0.9
tensorflow : 1.3

| Instance type | GPU-name / memory | price | local | Compute Capability | 
| :-: | :-: | :-: | :-: | :-: |
| g2.2xlarge | GRID K520 / 4G | $0.1597 | Tokyo | 3.0 |
| g3.4xlarge | Tesla M60 / 8G | $0.2137 | Tokyo / N.Virginia | 5.2 |


# SSH Command 
$ ssh -i my.pem account@aws.com
```
ssh -i /Users/jacky/Downloads/aws-tokyo.pem ubuntu@ec2-13-112-251-86.ap-northeast-1.compute.amazonaws.com
```

# SCP Command 
$ scp -i my.pem my.file account@aws.com:destination_folder
```
scp -i /Users/jacky/Downloads/aws-tokyo.pem /Users/jacky/GitHub/ML2017FALL/hw3.zip ubuntu@ec2-13-112-251-86.ap-northeast-1.compute.amazonaws.com:/home/ubuntu
```

# unzip file
```
sudo apt-get install unzip
unzip file.zip -d destination_folder
```

# Install Nvidia Driver

```
sudo add-apt-repository ppa:graphics-drivers/ppa -y
sudo apt-get update
sudo apt-get install -y nvidia-375 nvidia-settings
```

# Donwload & Install CUDA Toolkit v8.0

```
wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb
sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64-deb
sudo apt-get update
sudo apt-get install -y cuda nvidia-cuda-toolkit
```

# Donwload & Install cuDNN  v6.0

```
wget http://developer.download.nvidia.com/compute/redist/cudnn/v6.0/cudnn-8.0-linux-x64-v6.0.tgz
tar zxvf cudnn-8.0-linux-x64-v6.0.tgz 
sudo mv cuda/lib64/* /usr/local/cuda-8.0/lib64/
sudo mv cuda/include/* /usr/local/cuda-8.0/include/
```

# Environment Setting

```
root$ vim ~/.bashrc
#增加下面三行

export CUDA_ROOT=/usr/local/cuda-8.0
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64
export PATH=$PATH:$CUDA_ROOT/bin

root$ source ~/.bashrc
```

# Check  

```
nvidia-smi 
nvcc --version
```


# Install tensorflow-gpu & keras & pandas using pip
```
sudo apt-get install python3-pip

pip3 install tensorflow-gpu
pip3 install keras
pip3 install pandas
```

# Test using mnist dataset
```
git clone https://github.com/fchollet/keras.git
cd keras/examples
python mnist_cnn.py
```

# Reference 
[NVIDIA GPU Compute Capability Table](http://blog.csdn.net/JiaJunLee/article/details/52067962)
[Amazon EC2 Instance Types](https://aws.amazon.com/tw/ec2/instance-types/)
[從AWS搭一個GPU運算環境來玩tensorflow](http://terrence.logdown.com/posts/1267063-from-the-aws-a-gpu-environment-to-play-tensorflow)
[AWSのGPUインスタンスにTensorflow/Keras環境を構築する 2017年6月版](https://qiita.com/yagays/items/a8d4932a977127d7c34e)
[Install Keras (2.0.4) on Ubuntu (16.04) 筆記](https://medium.com/@ywchen88/install-keras-2-0-4-on-ubuntu-16-04-%E7%AD%86%E8%A8%98-9c278fe8759e)
[How To Choose GPU For Deep Learning](http://ai.easyapi.com/blog/view/107)

