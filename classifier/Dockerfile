# syntax=docker/dockerfile:experimental
FROM ubuntu:22.04
WORKDIR /app

ARG DEBIAN_FRONTEND=noninteractive

# Install base packages
RUN apt update && apt install -y \
    curl zip git lsb-release software-properties-common apt-transport-https vim wget \
    python3.10 python3.10-distutils python3.10-venv

# Install pip and setuptools
RUN wget https://bootstrap.pypa.io/get-pip.py && \
    python3.10 get-pip.py && \
    python3.10 -m pip install --upgrade pip==21.3.1 setuptools==62.6.0 && \
    rm get-pip.py

# Symlink so python3/pip3 point to Python 3.10
RUN rm -f /usr/bin/python3 /usr/bin/pip3 && \
    ln -s /usr/bin/python3.10 /usr/bin/python3 && \
    ln -s /usr/local/bin/pip /usr/bin/pip3

# Copy requirements and install
COPY requirements.txt .
RUN pip3 install -r requirements.txt

# Copy the rest of your training scripts
COPY . .

# Run training script
ENTRYPOINT ["python3", "-u", "train.py"]