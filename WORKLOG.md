# Work Log

This file records what was actually completed, the evidence observed, and the exact point from which to resume.

## 2026-09-01 — Session 1: First working Docker image

### Objective

Create the first version of a simplified P4-to-Git learning image using Alpine Linux and the Git-related tools needed by a future synchronization application.

### Files created

- `Dockerfile`

### Dockerfile used

```dockerfile
FROM alpine:3.20

RUN apk add --no-cache git git-lfs openssh
```

### Commands executed

Initial build attempt:

```bash
docker build -t p4-sync-learning:v1
```

Observed error:

```text
"docker buildx build" requires exactly 1 argument
```

Cause: the build context argument was missing.

Corrected build:

```bash
docker build -t p4-sync-learning:v1 .
```

The dot specified the current directory as the build context.

Image verification:

```bash
docker image ls p4-sync-learning
```

Observed locally:

```text
REPOSITORY         TAG   IMAGE ID       SIZE
p4-sync-learning   v1    caeff4e6f020   41.2MB
```

Git verification:

```bash
docker run --rm p4-sync-learning:v1 git --version
```

Observed result:

```text
git version 2.45.4
```

### What was proven

1. Docker successfully read the Dockerfile.
2. Alpine Linux 3.20 was used as the base.
3. Git, Git LFS, and OpenSSH were installed during the image build.
4. The image `p4-sync-learning:v1` was stored locally.
5. A temporary container created from the image could execute Git.
6. `--rm` removed the test container after it stopped.

### Exact stopping point

The image build and non-interactive Git verification are complete.

The interactive `-it` exercise was explained but its execution output has not yet been recorded.

### Resume command

```bash
docker run --rm -it p4-sync-learning:v1 sh
```

Then run inside the container:

```sh
cat /etc/os-release
git --version
git lfs version
ssh -V
exit
```

### Next milestone

After the interactive verification succeeds, add Python and create `p4-sync-learning:v2`.
