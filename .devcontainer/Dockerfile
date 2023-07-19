# Use base image
FROM pytorch:babel

# Variables from build-arg
ARG USERNAME
ARG USER_ID
ARG GROUP_ID

# Install sudo and other system packages (git is already installed)
RUN apt-get update && \
    apt-get install -y \
    sudo \
    htop \
    less \
    tmux
    
# Install required python packages
RUN pip install \
    ipython \
    black
 
# Create a new group
RUN groupadd -g ${GROUP_ID} ${USERNAME}

# Create the new user and add to the group
RUN useradd -m -d /home/${USERNAME} -u ${USER_ID} -g ${GROUP_ID} -s /bin/bash ${USERNAME}

# Add the user to the sudo group with an empty password
RUN echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    echo "${USERNAME}:" | chpasswd -e

# Switch to the non-root user
USER ${USER_ID}:${GROUP_ID}