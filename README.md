# Docker cmd shortcuts

Working in a containerized environment has many advantages, but the implementation is mostly cumbersome due to the command overhead and non-obvious configuration for hardware passtrough/acceleration.

These scripts are intended to remedy the situation, providing the following additional functionality to dockers `bash` cmd interface, while retaining docker's useful autocomplete feature.

* SSH key and configuration passtrough from host
* X11 passtrough with and without gpu support, even over SSH
* Common directory mount `/mnt` for easy data sharing between host and container
* Device passtrough (USB, sdcards, etc.)
* Seemless attachment to new shell and concurrent display output
* Default gpu passtrough for all containers
* Automatic disposal for unamed containers

## Installation

### Linux (bash)
1 click installation into `-o ~/.bash_completion`:

``` bash
curl https://raw.githubusercontent.com/timongentzsch/docker_shortcuts/master/cmd_shortcuts -o ~/.bash_completion && exec bash
```

>  **note:** Make sure your is added to `docker` group: `sudo usermod -aG docker $USER`

## MacOS (zsh)
mac sure you have `oh-my-zsh` installed: `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"` and activate `docker` plugin in `.zshrc`

``` bash
curl https://raw.githubusercontent.com/timongentzsch/docker_shortcuts/master/cmd_shortcuts -o ~/.zsh_completion && exec bash
```

## Usage

### Initialize a container

``` bash
drun [add. docker args] [image_name] [command]
```
#### Example:
`drun ubuntu:focal` will initialize an interactive terminal session from the provided image with GPU support

>  **note:** docker containers will use gpus by default; if runtime is not available pass `--gpus none`. Add. docker args needs to be provided as one string: ~~-v example:example~~ -v=example:example

### Build a container

``` bash
dbuild [add. docker args]
```
#### Example:
`dbuild -t test .` will build a docker image from local `Dockerfile` in local build context

### Attach to running container

``` bash
dshell [add. docker args] [container_name]
```
#### Example:
`dshell running_container` will attach an interactive terminal session to a running container

>  **note:** docker containers will be restarted when exited. If no container name is provided the most recent container is used.