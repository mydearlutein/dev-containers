# Base CUDA image download
FROM nvidia/cuda:11.8.0-cudnn8-devel-ubuntu20.04

# Timezone
ARG DEVIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul

# Install mandatory OS packages
RUN apt-get update && \
    apt-get install -y curl tzdata logrotate vim build-essential automake wget locales git bzip2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Korean language setting
RUN locale-gen ko_KR ko_KR.UTF-8 && \ 
    update-locale LANG=ko_KR.UTF-8
ENV LANGUAGE=ko_KR.UTF-8
ENV LANG=ko_KR.UTF-8

# Install Python 3.11
RUN apt-get update && \
    apt install -y software-properties-common && \
    add-apt-repository -y ppa:deadsnakes/ppa && \
    apt update && \
    apt install -y python3.11 python3.11-dev python3.11-distutils 
RUN curl -sS http://bootstrap.pypa.io/get-pip.py | python3.11
RUN cd /usr/bin && rm python3 && ln -s python3.11 python3

# Update Python package managers
RUN python3 -m pip install -U pip wheel setuptools 

# Install JupyterLab
RUN python3 -m pip install JupyterLab
COPY start_notebook.sh /start_notebook.sh
RUN chmod +x /start_notebook.sh

# Set initial working directory
WORKDIR /workspace

CMD ["./start_notebook.sh"]