# GentooWSL
Gentoo Linux on WSL (Windows 10 1803 or later) based on [wsldl](https://github.com/yuk7/wsldl)

[![Screenshot-2021-06-04-075435.png](https://i.postimg.cc/GhFsDmTq/Screenshot-2021-06-04-075435.png)](https://postimg.cc/56t0d13C)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) 
[![License](https://img.shields.io/github/license/sileshn/GentooWSL.svg?style=flat-square)](https://raw.githubusercontent.com/sileshn/GentooWSL/master/LICENSE)

## 💻 Requirements
* For x64 systems: Version 1903 or higher, with Build 18362 or higher.
* For ARM64 systems: Version 2004 or higher, with Build 19041 or higher.
* Builds lower than 18362 do not support WSL 2.
* Enable Windows Subsystem for Linux feature.
```cmd
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```
* Enable Virtual Machine feature
```cmd
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
* Download and install the latest Linux kernel update package from [here](https://www.catalog.update.microsoft.com/Search.aspx?q=wsl). Its a cab file. Open and extract the exe file within using 7zip/winzip/winrar.

For more details, check [this](https://docs.microsoft.com/en-us/windows/wsl/install-win10) microsoft document.

## Install
#### 1. [Download](https://github.com/sileshn/GentooWSL/releases/latest) installer zip file.

#### 2. Extract all files in zip file to same directory

#### 3. Run Gentoo.exe to extract rootfs and register to WSL
Exe filename is using to the instance name to register.
If you rename it, you can register with a different name and have multiple installs.

#### 4. First steps to perform after install
```shell
$ emerge --sync
$ emerge --update --deep --with-bdeps=y @world
$ emerge --update --deep --with-bdeps=y @system
```
#### 5. Create root password and new user
```shell
$ passwd
$ sed -i 's/# %wheel ALL=(ALL) ALL/%wheel ALL=(ALL) ALL/g' /etc/sudoers
$ useradd -g users -G wheel -s /bin/bash -m <username>
$ passwd <username>
```
Exit and set <username> as default user.
```shell
> Gentoo.exe config --default-user <username>
```

## How-to-Use(for Installed Instance)
#### exe Usage
```dos
Usage :
    <no args>
      - Open a new shell with your default settings.

    run <command line>
      - Run the given command line in that instance. Inherit current directory.

    runp <command line (includes windows path)>
      - Run the given command line in that instance after converting its path.

    config [setting [value]]
      - `--default-user <user>`: Set the default user of this instance to <user>.
      - `--default-uid <uid>`: Set the default user uid of this instance to <uid>.
      - `--append-path <true|false>`: Switch of Append Windows PATH to $PATH
      - `--mount-drive <true|false>`: Switch of Mount drives
      - `--default-term <default|wt|flute>`: Set default type of terminal window.

    get [setting]
      - `--default-uid`: Get the default user uid in this instance.
      - `--append-path`: Get true/false status of Append Windows PATH to $PATH.
      - `--mount-drive`: Get true/false status of Mount drives.
      - `--wsl-version`: Get the version os the WSL (1/2) of this instance.
      - `--default-term`: Get Default Terminal type of this instance launcher.
      - `--lxguid`: Get WSL GUID key for this instance.

    backup [contents]
      - `--tar`: Output backup.tar to the current directory.
      - `--reg`: Output settings registry file to the current directory.

    clean
      - Uninstall that instance.

    help
      - Print this usage message.
```


#### How to uninstall instance
```dos
> Gentoo.exe clean

```

## How-to-Build
GentooWSL can build on GNU/Linux or WSL.

`curl`,`bsdtar`,`tar`(gnu) and `sudo` is required for build.
```shell
$ make
```
