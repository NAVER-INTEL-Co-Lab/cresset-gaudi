# The Cresset Template for PyTorch on the Intel Gaudi

## Introduction

This repository is a template for getting started with using PyTorch on the
Intel Gaudi. It is based on the `ngc` service of the 
[Cresset](https://github.com/cresset-template/cresset) template.

The template is mostly targeted towards researchers who must change their
development environment frequently and customize many aspects.

## Getting Started
### Pre-Installation

1. Press the green "Use this Template" button to create a new repository!
2. Install the Docker engine on the host machine.
[Instructions for Ubuntu hosts](https://docs.docker.com/engine/install/debian/#install-using-the-repository)
3. Run `make install-compose` to install Docker Compose if necessary.
4. Install the Habana Docker Runtime on the host.

   3-1. Visit this [link](https://docs.habana.ai/en/latest/Installation_Guide/Bare_Metal_Fresh_OS.html)
   for installation instructions.
   
   3-2. Go to "Install Using Containers" and install according to the host platform.

### Setup
1. Run `make env` to create a `.env` file. This need only be done once per directory.
2. Run `make build` to build the Docker image and start the container.
Run this command when you wish to rebuild the Docker image.
3. Run `make up` if the image has already been built and you do not wish to rebuild.
Note that this will delete the previous container, deleting any operations performed on it.

When configuring the environment, editing the `.env` file is
recommended over directly editing the `docker-compose.yaml` file.

For example, if the Synapse AI version for the project is to be updated,
add the following lines to the `.env` file.

```text
PYTORCH_VERSION=2.3.1
SYNAPSE_VERSION=1.17.1
```

Visit https://developer.habana.ai/catalog/pytorch-container
for PyTorch images available for the Intel Gaudi.

### Add Directories
1. Run `make over` to add a new directory to the container.
2. Edit the `docker-compose.override.yaml` file generated by the `make over`
command to mount desired host directories to the container.
Do not edit the `docker-compose.yaml` file if possible.

### How to Use
1. Run `make exec` to enter an existing Docker container.
2. Run `tmux` or related commands once inside the container
to prevent interruptions from disconnects.
3. Use ^d (cmd+d) to exit from the container.
This will not stop the container and `tmux` shells will continue to run.

## Modifying Requirements

1. To add `apt` packages to your project, edit the `apt.requirements.txt` file.
2. To add `conda` or `pip` packages to your project, edit the `environments.yaml` file.
3. Edit the `pip.uninstalls.txt` file to remove pre-installed `pip` packages on the image.
---
Note that `pip` packages installed on system Python have higher priority than
user-installed `pip` packages by design.

Use the `pip.uninstalls.txt` file to remove system `pip` packages if
custom versions of those packages are required.


## Using Cresset in an Existing Project

If the user wishes to use the template as a directory inside an existing project,
append `HOST_ROOT=..` to the `.env` file to configure the parent directory as the
root of the project on the host.

Other configurations using relative paths, such as `HOST_ROOT=../..` 
for the parent of the parent directory, are also possible.
