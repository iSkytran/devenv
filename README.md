# devenv

Dockerfiles for Development Environments

## Building

### Building the Base Image

The base image must be built first.

```bash
docker build base -t devenv:base
```

### Building the ROS 2 Image

```bash
docker build ros2 -t devenv:ros2
```

## Running

### Running the Base Image

```bash
docker run -it --name base -v $HOME/code:$HOME/code devenv:base
```

### Running the ROS 2 Image

```bash
docker run -it --name ros2 -v $HOME/code:$HOME/code devenv:ros2
```
