# Windows Subsystem for Linux (WSL) for Open Source EDA tools

Windows Subsystem for Linux (WSL) is a feature of Windows that allows you to run a Linux environment on your Windows machine, without the need for a separate virtual machine or dual booting. With native X11 (graphics) support on WSL2, the latest WSL, in **Winodws 10 version 2004+ (Build 19041+)** or **Windows 11**, you can now run GUI apps including all the open-source EDA tools like **Sue2/xschem, ngspice, Magic, netgen**, and **iverilog**.

In this page we will share instructions for installing WSL2 on Winodws 10/11 and install the EDA tools on a **Ubuntu 22.04** distribution.
  
## Install WSL
- **RESOURCES**:
  - For detail steps, follow these [instructions](https://learn.microsoft.com/en-us/windows/wsl/install) at [https://learn.microsoft.com](https://learn.microsoft.com/en-us/windows/wsl)
  - https://kwantaekim.github.io/2024/05/25/OSE-Docker/#wsl
- **Prerequisites**: Winodws 10 version 2004+ (Build 19041+) or Windows 11
- **Enabling WSL** : `Control Panel -> Programs -> Programs and Features -> Turn Windows Features On and Off` and **Select** `Windows Subsystem for Linux`  (This is a good [video](https://kwantaekim.github.io/2024/05/25/OSE-Docker/#wsl) for it. **NOTE** Do not follow this video to install distribution which it suggests to do through MS Store)
- If you have a previous WSL installed without your knowledge or, you've installed in from the _Microsoft Store_, it's best you **uninstall** it using the Windows "Add/remove Programs" app and/or `wsl --uninstall`
  - Some resources to [Uninstall legacy version of WSL](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting#uninstall-legacy-version-of-wsl) or [unregister or uninstall a Linux distribution](https://learn.microsoft.com/en-us/windows/wsl/basic-commands#unregister-or-uninstall-a-linux-distribution).
- It is also **highly recommended** to ensure **Virtualization (VTx)** is enabled in your BIOS. See [instructions here](https://www.laptopmag.com/articles/access-bios-windows-10) on how to access BIOS in a modern Windows 10 workstation/laptop. 
- Open PowerShell or Windows Command Prompt in **ADMINISTRATOR** mode by right-clicking and selecting "Run as administrator"
- In the PowerShell type `wsl --list --online`
  - This will list all the available distributions online. 
- To install a particular distribution (Distro) say `Ubuntu-22.04` (The name has to be exactly as printed in the above command):
  - `wsl --install -d Ubuntu-22.04`
  - You'll be asked to create an **username** and **password**. Keep the password safe which you need for all _root_ activities.
    - This account will be your default _user_ for the distribution and automatically sign-in on launch.
    - This account will be considered the Linux administrator, with the ability to run *sudo* (Super User Do) administrative commands.
    - To change or reset your password, in your Linux terminal type `passwd`.
    - If you forgot the password for your Linux distribution execute `wsl -u root` in a PowerShell.
      - If If you need to update the forgotten password on a distribution that is not your default, use the command: `wsl -d <DistroName> -u root`
    - See [Best practices for setting up a WSL development environment](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#set-up-your-linux-username-and-password) guide for a step-by-step walk-through of how to set up a user name and password for your installed Linux distribution(s), using basic WSL commands, installing and customizing Windows Terminal, set up for Git version control, code editing and debugging using the VS Code remote server, good practices for file storage, setting up a database, mounting an external drive, setting up GPU acceleration, and more.
  - **NOTE** You can install multiple Distros using the above command.
- It's important to update the WSL now by typing the following in the Powershell:
  - `wsl --update`
- And shut it down: `wsl --shutdown`. Note: it will automatically start when the WSL distro selected from the Windows menu.
- Once the installation is complete, the Linux distro will be available using the **Windows Start** under the name of the distro eg. `Ubuntu 22.04`. It's good idea to pin the application to Start or Desktop for ease of access.  
- When you access your linux terminal for the first time, make sure you update the distro:
  - `sudo apt update && sudo apt upgrade` to upgrade packages. It's a good idea to do this regularly.
- **Setting up Windows Terminal (optional)**: Although optional, highly recommended for include multiple tabs, panes, Unicode and UTF-8 character support, a GPU accelerated text rendering engine, and the ability to create your own themes and customize text, colors, backgrounds, and shortcuts.
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


