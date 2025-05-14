FROM ros:kinetic-perception

# Force older VS Code server version
ENV VSCODE_SERVER_VERSION=1.85.2

# Install newer libstdc++ for VS Code compatibility
RUN apt-get update && apt-get install -y \
    software-properties-common \
    && add-apt-repository -y ppa:ubuntu-toolchain-r/test \
    && apt-get update \
    && apt-get install -y libstdc++6=12.3.0-1ubuntu1~16.04 \
    && rm -rf /var/lib/apt/lists/*

# Create non-root user (required for dev containers)
RUN useradd -m -s /bin/bash container_user && \
    echo "container_user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# ROS Kinetic base setup
RUN apt-get update && apt-get install -y \
    python-catkin-tools \
    ros-kinetic-cv-bridge \
    ros-kinetic-tf \
    && rm -rf /var/lib/apt/lists/*

# Bypass VS Code server checks
RUN mkdir -p /home/container_user/.vscode-server/bin \
    && touch /tmp/vscode-skip-server-requirements-check

USER container_user
WORKDIR /home/container_user/catkin_ws
