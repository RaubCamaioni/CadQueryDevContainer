FROM ubuntu:20.04

# dependencies
RUN apt-get update && apt-get install -y \
    curl \
    libglu1-mesa libgl1-mesa-dri mesa-common-dev libglu1-mesa-dev \
    git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# mamba
WORKDIR /root
RUN curl -L -o mambaforge.sh "https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-$(uname)-$(uname -m).sh"
RUN bash mambaforge.sh -b -p $HOME/mambaforge
RUN rm mambaforge.sh

# install cadquery and cq-editor
RUN . /root/mambaforge/bin/activate \
    && conda create -y -n cq python \
    && conda activate cq \
    && mamba install -y -c cadquery cq-editor=master \
    && conda clean -a -y

RUN echo "source /root/mambaforge/bin/activate" >> /root/.bashrc
RUN echo "conda activate cq" >> /root/.bashrc