# devenv
Dockerfiles for Development Environments

## Building

### Building the Base Image

The base image must be built first.

```bash
docker build . -f  Dockerfile.base -t devenv:base
```

### Building the ROS 2 Image

```bash
docker build . -f  Dockerfile.base -t devenv:base
```

## Running

### Running the Base Image

```bash
docker run -it --name base -v $HOME/code:$HOME/code devenv:base
```

### Running the ROS 2 Image

```bash
docker run -it --name base -v $HOME/code:$HOME/code devenv:ros2
```
