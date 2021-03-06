---
title: Linux cheatsheet
is_recommended: true
category: Linux
tags: ["linux", "cheetsheet"]
---

This is more of a Ubuntu cheatsheet than a Linux one. However, many shortcuts and commands are usable on other Linux systems.

Most of these are just example usages. You should check each command's manual for more options (by using the `man` command).

# Basics

* Read the manual of any (supported) command

    ```
    man <command>
    ```

* Change the current directory

    ```
    cd <path>
    ```

    Go to home directory

    ```
    cd
    ```

* Print the current working directory

    ```
    pwd
    ```

* List files

    ```
    ls # List files in the current directory
    ls </path> # List files in a directory
    ls *.md # List files whose extention is `md`
    ls favicon* # List files that starts with `favicon`
    ls -l # List files with more information, like mod, size, owner
    ls -a # List all files, including hidden files
    ```

# Bash shortcuts

* Stop current command: `<Ctrl> + C`
* Sleep program: `<Ctrl> + Z`
* Go to start of line: `<Ctrl> + A`
* Go to end of line: `<Ctrl> + E`
* Cut from start of line: `<Ctrl> + U`
* Cut to end of line: `<Ctrl> + V`
* Select text: hold `<Shift>`, left click then drag your mouse
* Copy selection: `<Ctrl> + <Shift> + C`
* Paste selection: `<Ctrl> + <Shift> + V`
* Search for a previously used command: `<Ctrl> + R`
* Repeat last command: `!!`

# Users and permissions

* Check current user's name

    ```
    whoami
    ```

* Check the id of a user

    ```
    id <username>
    ```

* Run a command as root

    ```
    sudo <command>
    ```

* Run a command as another user

    ```
    sudo -u <username> <command>
    ```

* Switch to another user

    ```
    su <username> # This requires the user's password
    sudo su <username> # Root can switch to any user without knowing the password
    ```

* Add a new user

    ```
    sudo adduser <username>
    ```

* Add a user into a group

    ```
    sudo usermod -aG <groupname> <username>
    sudo adduser <username> <groupname>
    ```

* Delete a user

    ```
    sudo userdel <username>
    ```

* Change the user's password

    ```
    passwd
    ```

    Change another user's password

    ```
    sudo passwd <username>
    ```

* Change mod of a file

    ```
    sudo chmod <mod> <filepath>
    ```

    Variations:

    ```
    sudo chmod 600 ~/.ssh/authorized_keys
    sudo chmod +x <path> # make file at <path> executable
    sudo chmod a+x <path> # make file at <path> executable for all users
    sudo chmod -R <mod> <directory_path> # Change mod for all files under <directory>
    ```

    Notes: In order to `cd` to a directory, the directory itself must be executable to the current user

# Environment variables

* Print all environment variables

    ```
    printenv
    ```

* Set an environment variables

    ```
    export VARIABLE_NAME=<value> # There should be no spaces before and after `=`
    ```

* Some useful environment variables:
    * `$USER`: Current user's name, same as output of `whoami`
    * `$UID`: Current user's id, same as output of `id -u $USER`
    * `$PWD`: Path of the current working directory, same as output of `pwd`
    * `$HOME`: Current user's home directory
    * `$PATH`: A set of directories where executable programs are located. These programs can be called directly without specifying the full path.

# Basic programming

* Create a variables

    ```
    VARIABLE_NAME=<value> # There should be no spaces before and after `=`
    ```

* Checking a variable's value

    ```
    echo $VARIABLE_NAME
    ```

* Using variables in commands

    ```
    ls $HOME
    cd $HOME
    ```

* Using the `stdin` output of a command as the argument of another command

    ```
    ls `pwd`
    ```

* Piping the output of one command as the input of another command

    ```
    command1 .... | command2 ....
    ```

* Redirecting a file or stream

    ```
    command .... >/output.log 2>error.log
    command < file.txt
    ```

* Ignore error logs

    ```
    command arg1 arg2 arg3... 2>/dev/null
    ```

* Ignore all logs

    ```
    command arg1 arg2 arg3... >/dev/null 2>&1
    ```

* Run program in background (it's still killed if the terminal is closed)

    ```
    command arg1 arg2 arg3... &
    ```

# Files and folder

* Create an empty file

    ```
    touch filename
    ```

* Print content of a file

    ```
    cat </path/to/file>
    ```

* Quickly create a file with a short content

    ```
    echo "<?php phpinfo(); ?>" > phpinfo.php
    ```

* Appending content to file

    ```
    $ echo "1" > test
    $ echo "2" > test
    $ echo "3" >> test
    $ cat test
    2
    3
    $
    ```

* Count number of words in a file

    ```
    wc </path/to/file>
    ```

* Using `grep` to find a pattern in a file in directory

    ```
    grep <pattern> </path/to/file>
    ```

    Find pattern in all files in a directory recursively

    ```
    grep -r <pattern> </path/to/directory>
    ```

    Only show file names

    ```
    grep -rl <pattern> </path/to/directory>
    ```

    Search incasesensitively

    ```
    grep -i <pattern> </path/to/file>
    ```

* Using `find` to find a file

    ```
    find </path> -type f -name '<pattern>'
    ```

    Or finding a directory

    ```
    find </path> -type d -name '<pattern>'
    ```

* Check available diskspace

    ```
    df -ah
    du -sh
    ```

# System

* Show system and kernel

    ```
    uname -a
    ```

* Check system disk space usage

    ```
    df -h
    ```

* Show system date

    ```
    date
    ```

* Show uptime

    ```
    uptime
    ```

* Show current free and used memory in the system

    ```
    free -m
    ```

* Set the CPU affinity of a process

    ```
    taskset 0x01 command # Set the process's CPU's afinity to CPU 1
    taskset 0x03 command # Set the process's CPU's afinity to CPU 1 and 2
    taskset 0x07 command # Set the process's CPU's afinity to CPU 1, 2 and 3
    taskset 0x15 command # Set the process's CPU's afinity to CPU 1, 2, 3 and 4
    ...
    ```

    `01`, `03`, `07`, and `15` are just decimal values of `0001`, `0011`, `0111`, `1111`

* List all block devices (except RAM disks)

    ```
    lsblk
    ```

    This is useful to find the device path of your usb, sdcard, or hard drive.
    For example:

    ```
    NAME                  MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
    sda                     8:0    0 465,8G  0 disk
    ├─sda1                  8:1    0   487M  0 part /boot
    ├─sda2                  8:2    0     1K  0 part
    └─sda5                  8:5    0 465,3G  0 part
    ├─ubuntu--vg-root   252:0    0 457,4G  0 lvm  /
    └─ubuntu--vg-swap_1 252:1    0   7,9G  0 lvm  [SWAP]
    sdb                     8:16   1  14,6G  0 disk
    └─sdb1                  8:17   1  14,6G  0 part /media/usb
    sr0                    11:0    1  1024M  0 rom
    ```

    The device path of my usb's first partition is `/dev/sdb1`

* Mount a filesystem (i.e a usb drive, a hard drive...)

    ```
    sudo mount </device/path> </mount/point>
    ```

    Example:

    ```
    sudo mkdir /media/usb
    sudo mount /dev/sdb1 /media/usb
    ```

* Unmount a file system from a mount point

    ```
    umount </mount/point>
    ```
    Note: This only unmount the file system at the particular mount point, not all mount points that the file system is mounted to

* Eject a device

    ```
    sudo eject </device/path>
    ```

* Shutdown and restart

    ```
    sudo shutdown -P now # shutdown the machine
    sudo shutdown -r now # restart the machine
    ```

# Tips and tricks

* Use `tree` to visualize folder's structure

    ```
    tree <path>
    ```

    For example:

    ```
    $ tree ./
    ./
    ├── docker-compose.yml
    ├── logs
    ├── nginx
    │   └── site.conf
    └── www
        └── index.php
    ```

    However, `tree` must be installed first

    ```
    sudo apt-get install tree -y
    ```

* Use `watch` to execute a program periodically, then show the out put on the screen.

    ```
    watch -n <seconds> <command>
    ```

    For exampple: watch your memory usage every 5 seconds

    ```
    watch -n 5 free -m
    ```

* Use `htop` to monitor your system resource usage

    ```
    htop
    ```

    `htop` must first be installed

    ```
    sudo apt-get install htop
    ```

* Use `tmux` to multiplex your terminal

    ```
    sudo apt-get install tmux
    ```

* Shorthand command to resume your tmux session when available, else start a new session

    ``` sh
    TMUX_ALIAS="tfox"
    TMUX_SESSION_NAME="fox"
    alias "$TMUX_ALIAS"="(tmux has -t $TMUX_SESSION_NAME && tmux attach -t $TMUX_SESSION_NAME) || tmux new -s $TMUX_SESSION_NAME"
    ```

    Put the above script to your `~/.bashrc`, then everytime you want to use tmux, you can just type `tfox` instead.

* Connect to your tmux session when doing `ssh`. Start a new session if not available

    ``` sh
    TMUX_SESSION_NAME="fox"

    # Automatically start attach tmux session when under ssh
    if [ -n "$SSH_CLIENT" ] || [ -n "$SSH_TTY" ]; then
    if [[ "$TERM" != "screen" ]]; then
        (tmux has -t $TMUX_SESSION_NAME && tmux attach -t $TMUX_SESSION_NAME) || tmux new -s $TMUX_SESSION_NAME;
    fi
    fi
    ```

* Add the following command as keyboard shortcut (Fox example, `ScrollLock`) to toggle fullscreen mode of the currently focused window

    ```
    wmctrl -r ":ACTIVE:" -b toggle,fullscreen
    ```
