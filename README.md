# Dev Container Setup

This documentation explains the setup and configuration of the development container used for this project.

## .devcontainer Folder

The `.devcontainer` folder contains configuration files that define the development container environment.

### devcontainer.json

```json
{
    "name": "My Dev Container",
    "dockerFile": "Dockerfile",
    "context": "..",
    "workspaceFolder": "/workspace/TestDevContainers",
    "mounts": [
        "source=/home/rob/Documents/Labs/TestDevContainers,target=/workspace/TestDevContainers,type=bind"
    ],
    "settings": {
        "terminal.integrated.defaultProfile.linux": "bash"
    }
}
```

- **name**: A descriptive name for the container.
- **dockerFile**: Specifies the Dockerfile to use for building the container. This field tells VSCode to look for a file named `Dockerfile` in the `.devcontainer` folder.
- **context**: The build context for Docker, set to the parent directory in this case.
- **workspaceFolder**: The working directory inside the container where the project will be mounted (in this case set to my test directory).
- **mounts**: Bind mounts from link local folders to the the container
    - **`source`**: The local directory to be mounted.
    - **`target`**: The Directory inside the container where the local directory will be mounted.
    - **`type`**: Specifies that this is a bind mount.
- **settings**: VSCode settings to apply within the container, here setting the default terminal profile to `bash`


# Dockerfile

### .devcontainer/Dockerfile
```
FROM ubuntu:latest

### Install basic tools if needed
RUN apt-get update && apt-get install -y \
    build-essential \
    && apt-get clean

### Set the working directory
WORKDIR /workspace/TestDevContainers
```

- **FROM**: Specifies the base image for the container, here we use the latest Ubuntu image.
- **RUN**: Executes commands in the container to install necessary tools. Here, it installs `build-essential` which includes common development tools.
- **WORKDIR**: Sets the working directory inside the container where commands will be executed. This is the same directory specified in the `workspaceFolder` in `devcontainer.json`.

## How to Use

1. Open your project in VSCode.
2. Open the Command Platte (F1 or Ctrl+Shift+P).
3. Select "Dev Containers: Open Folder in Container...".
4. Choose your project directory.

VSCode will build and configure the development container based on the provided `Dockerfile` and `devcontainer.json` configuration files. 