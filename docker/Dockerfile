# Use an official pytorch runtime as a parent image
FROM pytorch/pytorch:1.6.0-cuda10.1-cudnn7-runtime

# Set the working directory to /app
WORKDIR /app

# Copy the environment.yml file to the container
COPY environment_docker.yml .

# Reinstall conda
RUN apt-get update && \
    apt-get install wget -y && \
    rm -rf /opt/conda && \
    mkdir /opt/conda && \
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O /opt/miniconda.sh && \
    bash /opt/miniconda.sh -b -u -p /opt/conda && \
    rm -rf /opt/miniconda.sh && \   
    /opt/conda/bin/conda init bash && \
    conda update --all -y && \
    conda --version

# Update the base environment based on the environment.yml file
RUN conda env update --name base --file environment_docker.yml

# Set the working directory to /home
WORKDIR /home
