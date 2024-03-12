# Windows Subsystem for Linux (WSL) for Open Source EDA tools

Windows Subsystem for Linux (WSL) is a feature of Windows that allows you to run a Linux environment on your Windows machine, without the need for a separate virtual machine or dual booting. With native X11 support on WSL2, the latest WSL, in **Winodws 10 version 2004+ (Build 19041+)** or **Windows 11**, you can now run GUI apps including all the open-source EDA tools like **Sue2, ngspice, Magic, netgen**, and **iverilog**.

In this page we will share instructions for installing WSL2 on Winodws 10/11 and install the EDA tools on a **Ubuntu 22.04** distribution.

**Table of Content**
- [Install WSL](#install-wsl)
- [Install Open Source EDA Tools](#install-open-source-eda-tools)
  
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
## Install Open Source EDA Tools
Once the WSL is setup, we are now ready to install the open source EDA tools. All the tools (except sue2) is available on Ubuntu 22.04 distro that you can install by simply typing `sudo apt install <toolName>`. We will install **Icarus Verilog** `iverilog` 
 and **GTKWave** `gtkwave` from the distro itself since it is pretty close to the latest release. For the rest of the tools, we have compiled version for *Ubuntu 22.04* on github that we are going to use to get the latest version.

- **PREREQUISITES**: `sudo apt install tcl tk libglu1-mesa`  packages/libraries required for sue2 and Magic.
- **INSTALLING iVerilog**:
  - [iVerilog creator Steve Icarus's document page](https://steveicarus.github.io/iverilog)
  - `sudo apt update && sudo apt upgrade -y` : To update your distribution
  - `sudo apt install iverilog gtkwave` : Install iverilog and viewer gtkwave
  - A quick start guide to get you started with iVerilog
    - Create project directory say `mkdir -p ~/iverilog/test` and `cd` to that directory.
    - `iverilog -o tb_mydut.vvp mydut.v tb_mydut.v` : Compile the verilog codes `mydut.v tb_mydut.v` and create an output `tb_mydut.vvp`
    - `vvp tb_mydut.vvp` : Convert the compiled output to a VCD format for GTKWave.
    - `gtkwave dump.vcd` : Note: the filename `dump.vcd` is assumed to be in `tb_mydut.v`
    - You can find an example code and it's testbench [here](https://github.com/silicon-vlsi/VLSI-2024).
- [**NGSPICE**](https://github.com/silicon-vlsi-org/eda-ngspice): See Download and Setup instruction in the [gitHub page](https://github.com/silicon-vlsi-org/eda-ngspice#downloading-&-setting-up-ngspice).
- [**Sue2+**](https://github.com/silicon-vlsi-org/eda-sue2Plus): See the instructions here on download and setup of schematic editor sue2+.
- [**MAGIC**](https://github.com/silicon-vlsi-org/eda-magic): See Download and Setup instruction in the [gitHub page](https://github.com/silicon-vlsi-org/eda-magic#downloading-&-setting-up-magic)
- [**NETGEN**](https://github.com/silicon-vlsi-org/eda-netgen): See Download and Setup instruction in the [gitHub page](https://github.com/silicon-vlsi-org/eda-netgen#downloading-&-setting-up-netgen)
- [**TECHNOLOGY**](https://github.com/silicon-vlsi-org/eda-technology): See Download and Setup instruction in the [gitHub page](https://github.com/silicon-vlsi-org/eda-technology)


