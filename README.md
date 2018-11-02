# About

Dockerfile forked from `tensorflow-notebook` in [docker-stacks](https://github.com/jupyter/docker-stacks) repository, modified to use GPU version of TensorFlow.

# Versions

* CUDA 9.2
* cuDNN 7
* TensorFlow 1.11
* Keras 2.2

# Example environment

## Operating System

* Ubuntu Desktop 16.04 LTS

## NVIDIA Graphic Card

* GeForce GTX 1080 Ti

## NVIDIA Graphic Driver

* nvidia-396

```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-396 -y
sudo reboot now
```

## Docker CE

https://docs.docker.com/install/linux/docker-ce/ubuntu/

```
sudo apt update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

sudo apt update
sudo apt install docker-ce -y
```

## NVIDIA Docker

https://github.com/NVIDIA/nvidia-docker

```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt update

sudo apt install  nvidia-docker2 -y
sudo pkill -SIGHUP dockerd
```

# Usage

## Build

```
git clone https://github.com/akimateras/tensorflow-notebook-gpu.git
docker build -t akimateras/tensorflow-notebook-gpu tensorflow-notebook-gpu
```

## Run

```
docker run -d \
    --runtime=nvidia \
    --name=jupyter-gpu \
    -p 8888:8888 \
    -v /your/notebook/directory:/home/jovyan \
    akimateras/tensorflow-notebook-gpu
```

Now you can open your notebook on http://localhost:8888/ .

You need access token to start using notebook.
It will be find from the internal log of container:

```
docker logs jupyter-gpu
```

If you want to know more detail, [original project](https://github.com/jupyter/docker-stacks) will be helpful.
