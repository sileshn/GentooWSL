# GentooWSL
Gentoo Linux on WSL (Windows 10 1803 or later) based on [wsldl](https://github.com/yuk7/wsldl)

![screenshot](https://github.com/sileshn/GentooWSL/blob/master/img/screenshot.png)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) ![License](https://img.shields.io/github/license/yuk7/AlpineWSL.svg?style=flat-square)

## 💻 Requirements
* For x64 systems: Version 1903 or higher, with Build 18362 or higher.
* For ARM64 systems: Version 2004 or higher, with Build 19041 or higher.
* Builds lower than 18362 do not support WSL 2.
* Enable Windows Subsystem for Linux feature.
* Download and install the Linux kernel update package from [here](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi).

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
      - Run the given command line in that distro. Inherit current directory.

    runp <command line (includes windows path)>
      - Run the path translated command line in that distro.

    config [setting [value]]
      - `--default-user <user>`: Set the default user for this distro to <user>
      - `--default-uid <uid>`: Set the default user uid for this distro to <uid>
      - `--append-path <on|off>`: Switch of Append Windows PATH to $PATH
      - `--mount-drive <on|off>`: Switch of Mount drives
      - `--default-term <default|wt|flute>`: Set default terminal window

    get [setting]
      - `--default-uid`: Get the default user uid in this distro
      - `--append-path`: Get on/off status of Append Windows PATH to $PATH
      - `--mount-drive`: Get on/off status of Mount drives
      - `--wsl-version`: Get WSL Version 1/2 for this distro
      - `--default-term`: Get Default Terminal for this distro launcher
      - `--lxguid`: Get WSL GUID key for this distro

    backup [contents]
      - `--tgz`: Output backup.tar.gz to the current directory using tar command
      - `--reg`: Output settings registry file to the current directory

    clean
      - Uninstall the distro.

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
