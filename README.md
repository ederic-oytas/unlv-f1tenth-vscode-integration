
# UNLV F1Tenth VSCode Integration

This guide will show you how to integrate VSCode within your Docker project. Doing this is completely **optional** for the course.

Doing this will provide you useful tools for your project:

* VSCode Editor - Graphical editor
* VSCode Extensions (linters, type checkers) - Very useful!

## Guide

First, install [Visual Studio Code](https://code.visualstudio.com/) if you haven't already.

Then, install the [Dev Containers VSCode Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) for VSCode.

Afterward, in VSCode, open the folder containing all of your ROS 2 workspaces (e.g. `sim_ws/`, `lab1_ws/`).

Then, from the folder root (not a workspace root), create a new file called `.devcontainer/devcontainer.json`.

![Screenshot of the files](devcontainer-files-in-vscode.png)

Then copy and paste the following contents inside:

```json
{
  // Name of container
  "name": "Ubuntu ROS2 Foxy F1Tenth",
  // Docker Compose file to use
  "dockerComposeFile": "../sim_ws/src/f1tenth_gym_ros/docker-compose.yml",
  // Service to work on (one of the services in the compose file)
  "service": "sim",
  // Path of the workspace folder inside the container
  "workspaceFolder": "/",
  "customizations": {
    "vscode": {
      // VSCode Extensions to install in the environment
      "extensions": [
        "ms-python.python",
        "ms-python.vscode-pylance",
        "ms-python.debugpy",
        "ms-azuretools.vscode-docker",
        "charliermarsh.ruff",
        "ms-python.black-formatter"
      ],
      // Settings
      "settings": {
        "[python]": {
          "editor.defaultFormatter": "charliermarsh.ruff",
          "editor.formatOnSave": true
        },
        "python.analysis.include": [
          "/lab?_ws/src/**/*",
          "/sim_ws/src/**/*"
        ]
      }
    }
  }
}
```

This is a configuration file for the Dev Container, you can change some of the settings if you want to alter some of the settings. For more information, see the [VSCode Dev Containers documentation](https://code.visualstudio.com/docs/devcontainers/containers).

Once you have finished copy and pasting, go to the Command Palette (use `Ctrl+Shift+P` or **Run > Command Palette**). Then, type in and enter **Dev Containers: Rebuild and Reopen in Container**. This will build the docker container and make your VSCode window open *inside* the container.

And you are set up!

## Commands

Some useful commands to know *outside* the container:

* **Dev Containers: Rebuild and Reopen in Container**: Builds and opens in container.
* **Dev Containers: Reopen in Container**: Opens in container without rebuilding.
* **Dev Containers: Rebuild Without Cache and Reopen in Container**: Completely rebuild and reopen in container.

A useful command to use *inside* the container:

* **Dev Containers: Reopen Folder Locally**: Opens outside the container (locally).

## Resources

* VSCode Dev Containers:  https://code.visualstudio.com/docs/devcontainers/containers
