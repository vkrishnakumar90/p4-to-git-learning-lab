# Docker Foundation for the P4-to-Git Learning Image

## Objective

Build the first layer of a simplified P4-to-Git synchronization image and verify that the required Git tools are available inside its containers.

## Core relationship

```text
Dockerfile → builds an image → image creates containers
```

- A **Dockerfile** is the recipe.
- An **image** is the prepared, immutable package produced by the build.
- A **container** is a running instance created from an image.

## Alpine Linux

Alpine is a small Linux distribution commonly used as a Docker base image.

```dockerfile
FROM alpine:3.20
```

This means:

> Start building the image using Alpine Linux 3.20.

## musl and glibc

Linux programs use a C library for common low-level operations such as file access, memory management, process creation, and networking.

Standard Alpine uses a small C library called **musl**.

Many precompiled Linux applications expect **glibc**, the GNU C Library. A native executable built for glibc may not run correctly in a standard Alpine environment containing only musl.

In a later milestone, this becomes relevant when adding and testing a Perforce client. The current image does not contain the Perforce CLI yet.

## apk

`apk` is Alpine Linux's package manager.

```sh
apk add git
```

This installs Git into the Alpine environment.

Comparable package managers include:

```text
Ubuntu/Debian → apt
Red Hat       → dnf or yum
Alpine        → apk
```

## --no-cache

```sh
apk add --no-cache git
```

`--no-cache` prevents the downloaded package catalogue from being retained after installation. This helps keep the image smaller.

## RUN

```dockerfile
RUN apk add --no-cache git git-lfs openssh
```

`RUN` executes the command while Docker builds the image. The installed software becomes part of the resulting image, so containers created from that image already contain the tools.

This differs from manually installing software inside a running container:

```text
Manual apk add inside a container
→ changes only that container

RUN apk add inside the Dockerfile
→ becomes part of the newly built image
```

## Installed tools

- **Git** performs repository operations such as detecting changes, committing, branching, and pushing.
- **Git LFS** supports large files managed using Git Large File Storage.
- **OpenSSH** supports secure connections and SSH-based Git authentication.

## Building the image

```bash
docker build -t p4-sync-learning:v1 .
```

| Part | Meaning |
|---|---|
| `docker build` | Build a Docker image |
| `-t` | Assign an image name and tag |
| `p4-sync-learning` | Image name |
| `v1` | Version tag |
| `.` | Use the current directory as the build context |

Without the final dot, Docker does not know which directory or context to use for the build.

## Checking the local image

```bash
docker image ls p4-sync-learning
```

This lists local images matching the name `p4-sync-learning`.

## Running one command

```bash
docker run --rm p4-sync-learning:v1 git --version
```

This creates a temporary container, runs `git --version`, displays the result, and stops.

- `docker run` creates and starts a container.
- `--rm` automatically removes the container after it stops.
- `p4-sync-learning:v1` selects the image.
- `git --version` is the command executed inside the container.

An interactive terminal is unnecessary when running only one command.

## Interactive mode

```bash
docker run --rm -it p4-sync-learning:v1 sh
```

- `-i` keeps standard input open.
- `-t` allocates a terminal.
- `sh` starts Alpine's shell.
- `--rm` removes the container after exit.

Inside the container, multiple commands can be executed:

```sh
cat /etc/os-release
git --version
git lfs version
ssh -V
exit
```

## Verified result

The image built successfully, and a temporary container returned:

```text
git version 2.45.4
```

This proves that Git was installed into the image and is available to containers created from it.

## Key takeaway

> The first version of the learning image uses Alpine Linux as its base and installs Git, Git LFS, and OpenSSH during the build. Docker can create temporary containers from the image and execute the installed tools.
