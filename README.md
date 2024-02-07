# Debugging Ren'py with PowerShell for Visual Studio Code

This template includes VSCode launchs for developing Ren'Py projects.

**What can be done**:
* Add `$ print("...")` to display them in the vscode terminal while the app is running
* Don't have to open Ren'py SDK every time
* Close the game with CTRL+C in the terminal or when closing VSCode

**What cannot be done**:
* Insert breakpoint

## Install
* [Install PowerShell on Windows, Linux, and macOS](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell?view=powershell-7.4)
* [Install PowerShell Extension for VS Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell)
* Download [Ren'Py SDK](https://www.renpy.org/) and extract into the folder
* Add files into your project

## How Run Debug
As shown in the image there are several launches that are added


![image](https://user-images.githubusercontent.com/67595890/179401467-c8abbc9b-8970-4bad-af86-2b5b31c173a4.png)


In any case, if you have never used VS Code Debugging I recommend you read first: [Debugging](https://code.visualstudio.com/docs/editor/debugging)

### Setup

( **Necessary only in the beginning** )

It will create the .renpy-sdk file in which the path to your Ren'Py SDK folder is written.

After you launch it, paste the path to your Ren'Py SDK folder
Exemple: `/home/username/renpy`

### Run

Select:

- Run or
- Force Recompile & Run

And Play!


## Possible problems

### A strange error screen opens (tiny file dialogs)

![image](https://user-images.githubusercontent.com/67595890/181924847-19e28398-259a-4ca0-831a-da72410e4612.png)

This happens when renpy tries to open the error file and the operating system does not have a program capable of opening a txt from the terminal.

The solution is to install a program to open these files. For example yad

```bash
sudo apt-get install -y yad

```

### After an error CTRL+C doesn't work

This happens in case the error log is opened for editing with VIM.


In this case you must write the following sequence of characters to close the file: `:q`


## Linux commands

### Give renpy permission

Almost certainly when you start debugging for the first time, it will give you an error because some files do not have "authorization" to be executed.

To fix this you need to run the following commands in the Renpy SDK folder

```bash
chmod +x renpy.sh
chmod +x renpy.py
chmod +x renpy.exe
chmod +x lib/py3-linux-x86_64/renpy
chmod +x lib/py3-linux-x86_64/pythonw
sudo apt-get install -y xdg-utils

```

### Installing PowerShell on Ubuntu
https://learn.microsoft.com/en-us/powershell/scripting/install/install-ubuntu?view=powershell-7.3
```bash
# Update the list of packages
sudo apt-get update
# Install pre-requisite packages.
sudo apt-get install -y wget apt-transport-https software-properties-common
# Download the Microsoft repository GPG keys
wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb"
# Register the Microsoft repository GPG keys
sudo dpkg -i packages-microsoft-prod.deb
# Update the list of packages after we added packages.microsoft.com
sudo apt-get update
# Install PowerShell
sudo apt-get install -y powershell
```

## Use microsoft wsl

You can also debug on WSL.


But there might be some problems while opening the GUI of WSL. It depends on the compatibility with your graphics card. Read: https://docs.microsoft.com/it-it/windows/wsl/tutorials/gui-apps



## Files

- `bin/renpy.ps1`: Script for calling Ren'Py SDK
- `bin/set-origin.sh`: Git setup helper to configure your local folder to sync to a remote host
- `.vscode/launch.json`: Launch for launching Ren'Py SDK commands without opening the Ren'Py launcher.
  - Setup (custom file for remembering your project's SDK path for commands to work)
  - Run
  - Force Recompile & Run
  - Delete Persistent
  - Lint
  - Distribute
