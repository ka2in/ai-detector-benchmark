# Docker Primer for the Impatient

Containerization has become a prerequisite for any developer shipping software today. This primer covers Docker essentials, from installing the engine to running your first container. This primer is written for developers using container-based workflows.

## Short introduction

Docker is a containerization platform. A containerization platform allows you to perform a number of essential tasks, including:

- shipping an application with its dependencies
- running that application consistently across different machines
- isolating processes so they do not interfere with each another
- distributing pre-built images through a shared registry

Since its launch in 2013, Docker has popularized the idea of lightweight, portable containers. Unlike a virtual machine, a Docker container shares the host machine's kernel, which makes it faster to start while reducing resource-consumption.

With Docker, you do not need to install an application's full dependency chain directly on your machine. The image itself contains everything the application needs. This is also why Docker has become a common building block in continuous integration and deployment pipelines.

## Docker concepts

A typical Docker workflow consists of three core objects:

- Image: a read-only template that contains the application code, runtime, libraries, and configuration needed to run it.
- Container: a running instance of an image. You can create, start, stop, and delete containers independently of the image they originated from.
- Registry: a storage and distribution system for images, such as Docker Hub or a private registry.

## Installation on Linux

To install Docker on Debian-based distributions, run the following commands:

```
$ sudo apt-get update
$ sudo apt install docker.io
```

For Red Hat-based distributions, use the following commands:

```
$ sudo dnf update
$ sudo dnf install docker
```

## Initial configuration

After installing Docker, you must add your user to the `docker` group so you do not need to use `sudo` for every single command:

```
$ sudo usermod -aG docker $USER
```

You will need to log out and back in to apply this change. To confirm Docker is installed correctly, run:

```
$ docker --version
```

## Docker essential commands

Here are the most essential commands that will get you up and running within minutes.

### Pulling an image

To download an image from a registry without running it, use the command:

```
$ docker pull <image>
```

For example, to pull the official Nginx image, run the command:

```
$ docker pull nginx
```

### Running a container

To create and start a container from an image, type this command:

```
$ docker run <image>
```

To run the container in the background, add the `-d` flag:

```
$ docker run -d nginx
```

### Listing containers

To view all currently running containers, type:

```
$ docker ps
```

To view all containers, including stopped ones, use the `-a` flag:

```
$ docker ps -a
```

### Stopping and removing containers

To stop a running container, use its container ID or name:

```
$ docker stop <container>
```

To remove a stopped container:

```
$ docker rm <container>
```

### Viewing logs

To inspect the output of a running or stopped container, type the command:

```
$ docker logs <container>
```

The `-f` flag allows you to stream logs continuously as new lines are produced:

```
$ docker logs -f <container>
```

## Building your own image

Most projects define their own image using a `Dockerfile`. This is a plain text file that describes how the image should be built. Here's a minimal example of a `Dockerfile`:

```
FROM node:20
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
```

To build an image from a Dockerfile in your current directory, run this command:

```
$ docker build -t my-app .
```

The `-t` flag tags the resulting image with a name. This makes it easier to reference later.

## Managing volumes

Containers are ephemeral by default: any data written inside them disappears once the container is removed. To make data persistent across container restarts, Docker uses volumes.

To create a named volume, run this command:

```
$ docker volume create my-data
```

To mount that volume into a container, use the `-v` flag when starting it:

```
$ docker run -v my-data:/app/data my-app
```

## Cleaning up

Unused images, stopped containers, and dangling volumes accumulate on your system Over time. To clean-up all of these in a single step, run:

```
$ docker system prune
```

Pay attention when using this command, since it will remove any container, image, or volume that's not actively in use.
