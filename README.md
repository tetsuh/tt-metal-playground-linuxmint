# tt-metal Playground for Linux Mint

This repository provides a self-contained environment for building the [tenstorrent/tt-metal](https://github.com/tenstorrent/tt-metal) on specific versions of Linux Mint. It uses Docker and GitHub Actions to create reproducible build environments compilation process.

## Workflows

This repository contains two main GitHub Actions workflows:

### 1. Build and Push Linux Mint Docker Image (`docker-build.yaml`)

This workflow builds a Docker image for a specific version of Linux Mint (`linuxmint22.1` or `linuxmint21.3`). This image serves as the base environment for compiling `tt-metal`.

* **Trigger**: Manually via `workflow_dispatch`.
* **Inputs**:
  * `target_os` (choice, default: `linuxmint22.1`): The Linux Mint version to build the Docker image for.
  * `push_image` (boolean, default: `true`): If checked, the built image will be pushed to the GitHub Container Registry (GHCR) for this repository.

### 2. Build tt-metal on Linux Mint (`build-tt-metal.yaml`)

This workflow uses one of the Docker images created by the **Build and Push Linux Mint Docker Image** workflow to check out and build a specific version of the `tt-metal` library.

* **Trigger**: Manually via `workflow_dispatch`.
* **Inputs**:
  * `target_os` (choice, default: `linuxmint22.1`): The Linux Mint version to use for the build.
  * `tt_metal_ref` (string, default: `main`): The branch, tag, or commit hash to check out from the `tenstorrent/tt-metal` repository.
