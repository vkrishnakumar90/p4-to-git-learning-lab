# P4-to-Git Learning Lab

A hands-on learning project to build a simplified P4-to-Git synchronization application from scratch.

## Learning objective

The completed learning application will demonstrate this general flow:

```text
Perforce repository
        ↓
Python synchronization application
        ↓
Local Git working tree
        ↓
Commit and push synchronized changes
```

This repository is an independent educational project. It does not contain proprietary application code, internal repository URLs, credentials, production logs, or confidential architecture.

## Current status

**Milestone 1 complete:** A small Docker image based on Alpine Linux was built with Git, Git LFS, and OpenSSH.

Current image used locally:

```text
p4-sync-learning:v1
```

The image was successfully built and Git was verified inside a temporary container.

## Repository guide

| File or directory | Purpose |
|---|---|
| `Dockerfile` | Builds the learning application image |
| `ROADMAP.md` | Tracks planned milestones |
| `WORKLOG.md` | Records completed work and the exact resume point |
| `notes/` | Detailed revision notes |
| `src/` | Python sync application, added in a future milestone |
| `scripts/` | Entrypoint and helper scripts, added later |
| `config/` | Safe example configuration, added later |
| `tests/` | Automated tests, added later |

## Current Dockerfile

```dockerfile
FROM alpine:3.20

RUN apk add --no-cache git git-lfs openssh
```

## Build locally

From the repository root:

```bash
docker build -t p4-sync-learning:v1 .
```

The final dot is the build context. It tells Docker to use the current directory and find the Dockerfile there.

## Verify the image

```bash
docker image ls p4-sync-learning
docker run --rm p4-sync-learning:v1 git --version
```

## Resume here

The next hands-on is to open an interactive shell and verify the installed tools:

```bash
docker run --rm -it p4-sync-learning:v1 sh
```

Inside the container:

```sh
cat /etc/os-release
git --version
git lfs version
ssh -V
exit
```

After verifying interactive mode, the next image version will add Python.
