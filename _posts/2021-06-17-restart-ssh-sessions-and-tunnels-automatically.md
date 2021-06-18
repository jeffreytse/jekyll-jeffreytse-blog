---
layout: post
title: Restart SSH Sessions and Tunnels Automatically
author: Jeffrey Tse
banner:
  image: https://wallpaperbat.com/img/79553-city-wallpaper-free-hd-download-hq.jpg
  opacity: 0.618
categories: computer
tags:
  - computer
  - linux
  - terminal
  - ssh
---

How many times have your SSH session suddenly interrupted while using SSH, and
then you have to reconnect it. Of course, the simplest solution is to use the
arrow keys to retrieve the previous command, and then press the Enter key.

This trick you have enjoyed for many years, is there a more elegant solution?
Today, I will introduce you a better solution to solve this problem, that is a
CLI tool named `autossh`.

## What's AutoSSH?

`autossh` is a program to start a copy of ssh and monitor it, restarting it as
necessary should it die or stop passing traffic. The idea is from rstunnel
(Reliable SSH Tunnel), but implemented in C.

Connection monitoring is done by using ssh to construct a loop of ssh
forwardings (one from local to remote, one from remote to local), and then sends
test data that it expects to get back. It backs off on the rate of connection
attempts when experiencing rapid failures such as connection refused.

## Install AutoSSH

If you don't have this program, please install it at first.

```BASH
# For ArchLinux
$ sudo pacman -S autossh

# For Debian/Ubuntu
$ sudo apt-get install autossh

# For CentOS/Fedora/RHEL
$ sudo yum install autossh

# For FreeBSD
$ pkg install autossh

# For OSX
$ brew install autossh
```

## Basic usage

```bash
$ autossh -M <port>[:echo_port] [-f] [SSH OPTIONS]
```

- `-M`: To specify the base monitoring port to use, or alternatively, to specify
  the monitoring port and echo service port to use.
  - When no echo service port is specified, this port and the port immediately
    above it (port# + 1) should be something nothing else is using.
  - `-M 0` will turn the monitoring off, and autossh will only restart ssh on
    ssh exit.
- `-f`: Causes autossh to drop to the background before running ssh.

Accordingly, we can use below command to automatically restart SSH tunnels:

```BASH
$ autossh -M 20000 -L 5000:localhost:5000 -C -N -T user@example.com
```

- `-C`: It forces compression of the connection, it's useful on modem lines and
  slow internet connections but if a fast connection is in place it will
  actually slow things down. Nowadays it should most likely be not used, unless
  your connection speed is terribly slow.
- `-N`: Do not execute a remote command. This is useful for just forwarding
  ports (protocol version 2 only).
- `-T`: Disable pseudo-tty allocation.

For monitoring port, the AutoSSH man page also recommends the second solution:

> -M [:echo_port],  
> …  
> In many ways this [ServerAliveInterval and ServerAliveCountMax options] may be
> a better solution than the monitoring port.

Alternative command:

```BASH
autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3"
```

## Booting as a systemd service

For systemd service, there is however an important thing to note from the
[document](http://www.freedesktop.org/software/systemd/man/systemd.service.html).

> Running programs in the background using “&”, and other elements of shell
> syntax are not supported.

The AutoSSH flag `-f` (background usage) already implies `AUTOSSH_GATETIME=0`,
however the flag `-f` is not supported by systemd.

Here is an example:

Create a systemd service configuration:

```bash
$ sudo vim /etc/systemd/system/autossh-tunnel.service
```

Content as below:

```ini
[Unit]
Description=AutoSSH tunnel service
After=network.target

[Service]
Environment="AUTOSSH_GATETIME=0"
ExecStart=/usr/bin/autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -N -L 5000:localhost:5000 -p 2222 user@example.com

[Install]
WantedBy=multi-user.target
```

Reload systemd for the new adding stuff:

```bash
$ sudo systemctl daemon-reload
```

Start the service

```bash
$ sudo systemctl start autossh-tunnel.service
```

Enable the service on booting:

```bash
$ sudo systemctl enable autossh-mysql-tunnel.service
```


## References

- [autossh - man page](https://www.harding.motd.ca/autossh/README.txt)
- [autossh - Automatically restart SSH sessions and tunnels](https://www.harding.motd.ca/autossh/)
- [How to reliably keep an SSH tunnel open?](https://superuser.com/questions/37738/how-to-reliably-keep-an-ssh-tunnel-open)
