# Docker Primer for the Impatient

Containerization is a core skill for anyone shipping software today. This primer covers Docker essentials, from installing the engine to running your first container, written for developers adopting container-based workflows.

## Short introduction

Docker is a containerization platform. Basically, a containerization platform allows you to perform a number of essential tasks, including:

- packaging an application together with its dependencies
- running that application consistently across different machines
- isolating processes so they do not interfere with one another
- distributing pre-built images through a shared registry

Docker was introduced in 2013 and popularized the idea of lightweight, portable containers, in contrast to full virtual machines. Unlike a virtual machine, a container shares the host machine's kernel, which makes it faster to start and lighter on resources.

With Docker, you do not need to install an application's full dependency chain directly on your machine, since everything the application needs ships inside the image. This is also why Docker has become a common building block in continuous integration and deployment pipelines.

## Docker concepts

In a typical Docker workflow, you will work with three core objects:

- Image: a read-only template that contains the application code, runtime, libraries, and configuration needed to run it.
- Container: a running instance of an image. You can create, start, stop, and delete containers independently of the image they came from.
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

After installing Docker, you should add your user to the `docker` group so you do not need to prefix every command with `sudo`:

```
$ sudo usermod -aG docker $USER
```

You will need to log out and back in for this change to take effect. To confirm Docker is installed correctly, run:

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

For instance, to pull the official Nginx image, you would type:

```
$ docker pull nginx
```

### Running a container

To create and start a container from an image, use the command:

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

To view all containers, including stopped ones, add the `-a` flag:

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

To inspect the output of a running or stopped container, use the command:

```
$ docker logs <container>
```

Adding the `-f` flag will stream logs continuously as new lines are produced:

```
$ docker logs -f <container>
```

## Building your own image

Most projects define their own image using a `Dockerfile`, a plain text file that describes how the image should be built. A minimal example looks like this:

```
FROM node:20
WORKDIR /app
COPY . .
RUN npm install
CMD ["npm", "start"]
```

To build an image from a Dockerfile in the current directory, run:

```
$ docker build -t my-app .
```

The `-t` flag tags the resulting image with a name, which makes it easier to reference later.

## Managing volumes

Containers are ephemeral by default, meaning any data written inside them disappears when the container is removed. To persist data across container restarts, Docker provides volumes.

To create a named volume, run:

```
$ docker volume create my-data
```

To mount that volume into a container, use the `-v` flag when starting it:

```
$ docker run -v my-data:/app/data my-app
```

## Cleaning up

Over time, unused images, stopped containers, and dangling volumes accumulate on your system. To remove all of these in one step, run:

```
$ docker system prune
```

Use this command with some caution, since it will remove any container, image, or volume that is not actively in use.
