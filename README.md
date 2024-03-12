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
  - This account will be considered the Linux administrator, with the ability to run *sudo* (Super User Do) administrative commands.
  - To change or reset your password, open the Linux distribution and enter the command: `passwd`.
  - If you forgot the password for your Linux distribution execute `wsl -u root` in a PowerShell.
    - If If you need to update the forgotten password on a distribution that is not your default, use the command: `wsl -d <DistroName> -u root`
- See [Best practices for setting up a WSL development environment](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#set-up-your-linux-username-and-password) guide for a step-by-step walk-through of how to set up a user name and password for your installed Linux distribution(s), using basic WSL commands, installing and customizing Windows Terminal, set up for Git version control, code editing and debugging using the VS Code remote server, good practices for file storage, setting up a database, mounting an external drive, setting up GPU acceleration, and more.
- Execute `sudo apt update && sudo apt upgrade` to upgrade packages.
- **Set up Windows Terminal**: Although optional, highly recommended for include multiple tabs, panes, Unicode and UTF-8 character support, a GPU accelerated text rendering engine, and the ability to create your own themes and customize text, colors, backgrounds, and shortcuts.
  - Install [Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/get-started) from the Microsoft Store.
  - [Use the Command Palette](https://learn.microsoft.com/en-us/windows/terminal/get-started#invoke-the-command-palette)
- **GUI Apps** is natively supported on WSL2 **Winodws 10 version 2004+ (Build 19041+)** or **Windows 11**. You can checkout this [Tutorial](https://learn.microsoft.com/en-us/windows/wsl/tutorials/gui-apps) for more info.
  - **TROUBLESHOOTING GUI PROBLEM**: If you find Linux GUI apps are distored and moving the pane makes it go away, disable the GPU accleration by adding a file (if it doesn't exit) to the location `C:\Users\<User>\.wslgconfig` and add the following content:

```bash
[system-distro-env]
;disable GPU in system-distro
LIBGL_ALWAYS_SOFTWARE=1
```

