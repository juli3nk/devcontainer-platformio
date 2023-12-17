# Platformio Devcontainer Template

This is a [VSC Devcontainer](https://code.visualstudio.com/docs/remote/containers) for [Platformio](https://platformio.org/) based on Debian Buster.

# **PlatformIO Development Container** for Visual Studio Code (Community)

## [devcontainer.json](./.devcontainer/devcontainer.json)

* Adds PlatformIO extension for VSCode
* Exposes port 8008 so that PIO Home isn't blank when opening a PIO Home tab in VSCode
* Mounts /dev so that Arduino devices on USB can read and written to
* Not sure `--privileged` is still necessary
- Uses default pio projects folder as workspace
- It uses Python 3.8.3
- Installs the nececessary udev rules

## [Dockerfile](./.devcontainer/Dockerfile)

* Installs Python and Clang dependencies
* Sets udev rules to allow non-root to write to arduino devices in /dev
* Sets a non-root user
* Installs PlatformIO CLI tools

## [settings.json](./.vscode/settings.json)

* Sets the PIO Home port to 8008 which is the port that's exposed in [devcontainer.json](./.devcontainer/devcontainer.json)


## How to use this devcontainer on GitHub Codespaces
Init platformio project. [board list](https://docs.platformio.org/en/latest/boards/index.html)

```bash
pio init --ide vscode --board <your board>
```

Login platformio account.

```bash
pio account login
```

[Remote MCU] Connect to the device.

```bash
pio remote agent start
``` 

[Codespace] List for remote devices.

```bash
pio remote device list
```

Flash and Monitor.

```bash
pio remote run --target upload --environment <your board>
pio remote device monitor 
```

### Adding the definition to your folder

1. If this is your first time using a development container, please see getting started information on [setting up](https://aka.ms/vscode-remote/containers/getting-started) Remote-Containers.
2. Clone this repository locally.
3. Start VS Code and open your project folder.
4. Use your local operating system's file explorer to drag-and-drop the locally cloned copy of the `.devcontainer` folder for this definition into the VS Code file explorer for your opened project.

After following these steps the contents of the `.devcontainer` folder in your project can be adapted to meet your needs.

1. Finally open the **Command Palette** and run **Remote-Containers: Reopen Folder in Container** to start using the definition.
