# Base image for Node.js and Electron development
FROM node:lts

# Install basic dependencies
RUN apt-get update && apt-get install -y \
  bash \
  git \
  curl \
  python3 \
  build-essential \
  libx11-dev \
  libxkbfile-dev \
  libsecret-1-dev \
  && rm -rf /var/lib/apt/lists/*

# Add a non-root user for development
ARG USERNAME=developer
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
  && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
  && apt-get install -y sudo \
  && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/$USERNAME \
  && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME
WORKDIR /workspace

# Install global npm tools for Electron development
RUN npm install -g electron electron-builder

# Set default command
CMD [ "bash" ]
