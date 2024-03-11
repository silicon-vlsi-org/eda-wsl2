# Windows Subsystem for Linux (WSL2) for Open Source EDA tools

Windows Subsystem for Linux (WSL) is a feature of Windows that allows you to run a Linux environment on your Windows machine, without the need for a separate virtual machine or dual booting. With native X11 support on WSL2 in **Winodws 10 version 2004+ (Build 19041+)** or **Windows 11**, you can now run GUI apps including all the open-source EDA tools like **Sue2, ngspice, Magic, netgen**, and **iverilog**.

In this page we will share instructions for installing WSL2 on Winodws 10/11 and install the EDA tools on a **Ubuntu 22.04** distribution.

## Install WSL
- For detail steps, follow these [instructions](https://learn.microsoft.com/en-us/windows/wsl/install) at [https://learn.microsoft.com](https://learn.microsoft.com/en-us/windows/wsl)
- **Prerequisites**: Winodws 10 version 2004+ (Build 19041+) or Windows 11
- Open PowerShell or Windows Command Prompt in **administrator** mode by right-clicking and selecting "Run as administrator", enter the `wsl --install` command, then **restart your machine**.
```PowerShell
wsl --install
```
- This command will enable the features necessary to run WSL and install the Ubuntu distribution (or other available distro) of Linux.
- **`NOTE`**: The above commands are for **first time** install.
  - `wsl -- list --online` for all available distros.
  - `wsl --install -d <DistroName>` To change the default Linux distro installed.
- To **uninstall** WSL, see [Uninstall legacy version of WSL](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting#uninstall-legacy-version-of-wsl) or [unregister or uninstall a Linux distribution](https://learn.microsoft.com/en-us/windows/wsl/basic-commands#unregister-or-uninstall-a-linux-distribution).
- Once installed, create **User Name** and **Password**:
  - This account will be your default user for the distribution and automatically sign-in on launch.
  - This account will be considered the Linux administrator, with the ability to run `sudo` (Super User Do) administrative commands.
- See [Best practices for setting up a WSL development environment](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#set-up-your-linux-username-and-password) guide for a step-by-step walk-through of how to set up a user name and password for your installed Linux distribution(s), using basic WSL commands, installing and customizing Windows Terminal, set up for Git version control, code editing and debugging using the VS Code remote server, good practices for file storage, setting up a database, mounting an external drive, setting up GPU acceleration, and more.
  - 
