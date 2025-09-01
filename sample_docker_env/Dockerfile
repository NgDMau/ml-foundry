FROM nvidia/cuda:12.6.2-cudnn-runtime-ubuntu22.04

# Set default shell to bash
SHELL ["/bin/bash", "-c"]

# Set up a working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y python3 python3-pip wget git git-lfs && rm -rf /var/lib/apt/lists/*

# Install Miniconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /tmp/miniconda.sh \
	&& bash /tmp/miniconda.sh -b -p /opt/conda \
	&& rm /tmp/miniconda.sh

# Add conda to PATH 
ENV PATH="/opt/conda/bin:$PATH"

# (Optional) Create a conda environment here if needed, e.g.:
# RUN conda create -n myenv python=3.10 -y

# (Optional) Activate environment in entrypoint or CMD if needed
CMD ["sleep", "infinity"]