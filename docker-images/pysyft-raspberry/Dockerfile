FROM arm32v7/python:3.6-slim-jessie

# Setup ENV for torch build
ENV NO_CUDA=1
ENV NO_DISTRIBUTED=1
ENV NO_MKLDNN=1
ENV NO_NNPACK=1
ENV NO_QNNPACK=1

# Install torch build deps
RUN apt update
RUN apt install -y \ 
		libopenblas-dev \
		libblas-dev m4 \
		cmake cython \
		python3-dev \
		python3-yaml \
		python3-setuptools

# Build torch 1.1
RUN apt install -y git
RUN git clone --recursive https://github.com/pytorch/pytorch --branch=v1.1.0
WORKDIR /pytorch
# Install more deps
RUN pip install pyyaml
RUN apt install -y software-properties-common
RUN add-apt-repository -y ppa:george-edison55/cmake-3.x
RUN apt update && apt upgrade
# RUN apt install cmake
# Continue build torch
RUN python3 setup.py build
RUN python3 setup.py install

# Install syft
RUN pip install --no-cache-dir syft

