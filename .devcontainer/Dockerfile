# .devcontainer/Dockerfile
FROM ubuntu:latest

# Install basic tools if needed
RUN apt-get update && apt-get install -y \
    build-essential \
    && apt-get clean

# Set the working directory
WORKDIR /workspace/TestDevContainers