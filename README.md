# ComfyUI-Setup

Setup scripts for ComfyUI.

# Installation

Download 'ComfyUI' related files.

*** Please change value of 'INSTALL_PATH'
    to be desired destination folder, by
    default install 'ComfyUI' to current
    folder. ***

```console
export INSTALL_PATH="."
export FULL_PATH=`readlink -f ${INSTALL_PATH}`/ComfyUI;

# Change directory to install path
cd ${INSTALL_PATH}

# Install 'ComfyUI'
git clone https://github.com/comfyanonymous/ComfyUI.git

# Change directory to 'custom_nodes' path
cd ComfyUI/custom_nodes

# Install 'ComfyUI-Manager'
git clone https://github.com/ltdrdata/ComfyUI-Manager.git
```

Build image then start the container.

*** Please change the 'CONTAINER_ID' to
    be desired container name, this name
    will be used to start/stop container
    in following commands. ***

```console
# Get your host's UID and GID
export IMAGE_ID="sd-comfy"
export CONTAINER_ID=${IMAGE_ID}
export HOST_UID=$(id -u)
export HOST_GID=$(id -g)

# For NVIDIA or RADEON
export DOCKER_FILE="Dockerfile.nvidia"
#export DOCKER_FILE="Dockerfile.radeon"

# Build the Docker image
docker build \
  --build-arg UID=${HOST_UID} \
  --build-arg GID=${HOST_GID} \
  -f ${DOCKER_FILE} \
  -t ${IMAGE_ID} \
  .

# Run the Docker container
docker run \
  -d \
  --gpus=all \
  --name ${CONTAINER_ID} \
  -v ${FULL_PATH}:/app \
  ${IMAGE_ID}

```

# Using the 'ComfyUI' container

Start the container.

```console
docker start ${CONTAINER_ID}
```

Stop the container.

```console
docker stop ${CONTAINER_ID}
```

Monitor the container.

```console
docker logs -f ${CONTAINER_ID}
```

