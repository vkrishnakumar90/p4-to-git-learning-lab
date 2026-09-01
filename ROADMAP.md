# Learning Roadmap

The project is intentionally developed in small milestones. Each milestone contains one concept, one hands-on exercise, verification evidence, and revision notes.

## Milestone 1 — Docker foundation

- [x] Create a dedicated learning project
- [x] Use Alpine Linux 3.20 as the base image
- [x] Install Git, Git LFS, and OpenSSH
- [x] Build `p4-sync-learning:v1`
- [x] Verify Git using a temporary container
- [ ] Verify all installed tools using an interactive `-it` session

## Milestone 2 — Python environment

- [ ] Understand why the sync application needs Python
- [ ] Install Python in the image
- [ ] Add a minimal `src/main.py`
- [ ] Build `p4-sync-learning:v2`
- [ ] Run the Python program inside a container

## Milestone 3 — Application packaging

- [ ] Add `requirements.txt`
- [ ] Understand `WORKDIR`
- [ ] Understand `COPY`
- [ ] Install Python dependencies
- [ ] Rebuild and verify the image

## Milestone 4 — Entrypoint

- [ ] Create `scripts/docker-entrypoint.sh`
- [ ] Understand `ENTRYPOINT`
- [ ] Pass container arguments to Python
- [ ] Verify argument flow from `docker run` to `main.py`

## Milestone 5 — Perforce client

- [ ] Understand the role of the `p4` CLI
- [ ] Add the Perforce client safely
- [ ] Examine native-library compatibility
- [ ] Compare Alpine `musl` with applications expecting `glibc`
- [ ] Verify the client without using enterprise credentials

## Milestone 6 — Git synchronization logic

- [ ] Create a safe local source fixture
- [ ] Detect changed files
- [ ] Copy changes into a Git working tree
- [ ] Create a commit
- [ ] Push to a disposable test repository

## Milestone 7 — Configuration and security

- [ ] Add `config.example.yaml`
- [ ] Read configuration in Python
- [ ] Pass safe runtime configuration
- [ ] Keep credentials out of the image and Git history
- [ ] Use mounted files or environment variables appropriately

## Milestone 8 — Reliability and tests

- [ ] Add structured logging
- [ ] Add error handling
- [ ] Make repeated synchronization idempotent
- [ ] Add unit tests
- [ ] Test common failure paths

## Milestone 9 — Operational understanding

- [ ] Connect image build and container execution
- [ ] Simulate a scheduled synchronization
- [ ] Document troubleshooting commands
- [ ] Compare the learning architecture with a generic enterprise deployment model
