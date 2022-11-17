FROM nvidia/cuda:11.3.1-devel-ubuntu18.04

# the usual
ENV DEBIAN_FRONTEND=noninteractive

# setup system, python and pip
RUN apt update && apt install -y software-properties-common git wget && add-apt-repository -y ppa:deadsnakes/ppa && apt update && apt install -y python3.10 python3.10-dev
RUN apt install -y curl
RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10
RUN pip3 install --upgrade pip

# the target version of pytorch
RUN pip3 install torch==1.12.1+cu113 torchvision==0.13.1+cu113 -f https://download.pytorch.org/whl/torch_stable.html

# the latest tinycudann
ARG CUDA_ARCHITECTURES
ENV TCNN_CUDA_ARCHITECTURES=$CUDA_ARCHITECTURES
RUN pip3 install git+https://github.com/NVlabs/tiny-cuda-nn/#subdirectory=bindings/torch

# nerfstudio
RUN pip3 install nerfstudio

# opencv
RUN pip3 uninstall -y opencv-python
RUN pip3 install "opencv-python-headless<4.3"