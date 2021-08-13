---
layout: post
title: How to Mount Remote Linux Filesystem
author: Jeffrey Tse
banner:
  image: https://wallpaperbat.com/img/90735-animated-landscape-2560x1440-wallpaper.png
  opacity: 0.75
categories: computer
tags:
  - computer
  - linux
  - terminal
---

If you want to mount remote file system on local for purposes like exploring,
programing, etc, I think this step-by-step guide on how to mount remote Linux
filesystem would be helpful for you.

## Mount Remote LINUX Filesystem

To mount remote Linux filesystem, you can use a tool named `sshfs`.
[SSHF](https://github.com/libfuse/sshfs) is a network filesystem client for
mounting remote directories over a Secure Shell connection.

### Install SSHFS

If you don't have this program, please install it at first.

```BASH
# For ArchLinux
$ sudo pacman -S sshfs

# For Debian/Ubuntu
$ sudo apt-get install sshfs

# For CentOS/Fedora/RHEL
$ sudo yum install sshfs

# For FreeBSD
$ pkg install sshfs

# For OSX
$ brew install sshfs
```

### Basic Usage


1.Create SSHFS Mount Directory/Point

```bash
$ mkdir /mnt/<local_folder>
```

2.Mount Remote Filesystem

```bash
$ sshfs user@host:/home/<remote_folder> /mnt/<local_folder>
```

Or specifying SSH options, for example:

```bash
# Using SSH key based authorization
$ sshfs -o "allow_other,IdentityFile=~/.ssh/id_rsa" user@host:/home/<remote_folder> /mnt/<local_folder>
```


Here's the accompanying [manpage](https://linux.die.net/man/1/sshfs), you would
learn more options for other usage.

3.Unmount Remote Filesystem

To unmount remote filesystem, just use the `umount` command as you usually do.

```bash
$ umount /mnt/<local_folder>
```

4.Mount on booting

To automatically mount remote filesystem on booting, you need to edit the file
called `/etc/fstab`, here we edit it through the editor called `vi`:

```bash
$ sudo vi /etc/fstab
```

Add new record on new line:

```txt
sshfs#user@host:/home/<remote_folder>/ /mnt/<local_folder> fuse.sshfs defaults 0 0
```

or with SSH options:

```txt
sshfs#user@host:/home/<remote_folder>/ /mnt/<local_folder> fuse.sshfs allow_other,IdentityFile=~/.ssh/id_rsa 0 0
```

Next, remount all in the fstab file to reflect the changes:

```bash
sudo mount -a
```

- `-a`: Mount all filesystems (of the given types) mentioned in fstab.

## References

- [sshfs(1) - Linux man page](https://linux.die.net/man/1/sshfs)
