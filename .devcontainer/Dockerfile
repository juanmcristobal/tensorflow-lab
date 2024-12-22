# Use the official Python image with TensorFlow pre-installed
# https://www.tensorflow.org/install/source#gpu
FROM tensorflow/tensorflow:2.17.0-gpu-jupyter

# Install additional dependencies, including sudo
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl git vim nano sudo && \ 
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Set up a non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME && \
    useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME && \
    mkdir -p /home/$USERNAME/.local && chown -R $USERNAME:$USERNAME /home/$USERNAME

# Grant sudo permissions to the user
RUN echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Grant write permissions to /etc
RUN chmod o+w /etc

# Set environment variables
ENV TF_ENABLE_ONEDNN_OPTS=0
ENV CUDA_VISIBLE_DEVICES=0

# Switch to the non-root user
USER $USERNAME
