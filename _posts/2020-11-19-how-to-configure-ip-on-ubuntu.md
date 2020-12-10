---
layout: post
title: How to configure IP on Ubuntu
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - network
  - terminal
---

## 1. Introduction

We often need to configure IP (static or dynamic), especially on newly
installed Ubuntu. However, since we have not systematically summarized
this, this makes our memory always a little confused, but it’s actually
very simple.

Here’s how to get networking all the way up in a matter of seconds
using just a few commands from the terminal.

## 2. Solutions

There are two ways to do this:

- Using ifconfig (DEPRECATED)
- Using ip and netplan (RECOMMEND)

And we also need to find out our network interface:

### 2.1 Identify Ethernet Interfaces

To quickly identify all available Ethernet interfaces, you can use the
`ip` command as shown below.

```bash
$ ip link
```

or

```bash
ip a
```

### 2.2 Using ifconfig

Configure Dynamic IP:

```bash
# Reset IP Address
$ ifconfig eth0 0.0.0.0 0.0.0.0

# Start DHCP
$ dhclient
```

Configure Static IP:

```bash
# Stop DHCP
$ killall dhclient

# Set Your IP Address
$ ifconfig eth0 192.168.1.100 netmask 255.255.255.0 up

# Set Your Default Gateway
$ route add default gw 192.168.1.1

# Set Your DNS Server
$ echo "nameserver 1.1.1.1" > /etc/resolv.conf
```

### 2.3 Using ip and netplan

Since `ifconfig` is being phased out, it’s time to get used to the
new system. By default, some Linux distribution (e.g. Ubuntu 18.04)
doesn’t use `ifconfig` anymore, and instead uses the new commands,
`ip` and `netplan`.

Firstly we need to configure network interface:

```bash
# Show your IP
$ ip addr show

# Bring an interface up or down
$ ip link set eth0 up/down

# Showing your routing
$ ip route show

# Show your DNS servers
$ systemd-resolve --status

# Show your network status
$ networkctl -a status
```

And then we edit our networking plan:

For Ubuntu, here’s the replacement for editing `/etc/networking/*`
in the old system. The whole system now uses YAML configuration
files under `/etc/netplan`.

```bash
$ vi /etc/netplan/99_config.yaml
```

Netplan configuration as below:

```yaml
network:
  renderer: networkd
  ethernets:
    eno1:
      addresses: [192.168.1.100/24] # for static IP
      gateway4: 192.168.1.1
      dhcp4: true # for dynamic IP
      optional: true
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]
  version: 2
```

And then to apply the configuration, run command as below:

```bash
$ netplan apply
```

### 2.4 Checking Network Connectivity

Assuming you have configured your network, now it's time for us to
check if you’re all set. Test by `ping` any domain name:

```bash
$ ping www.google.com
```

## 3. Conclusion

If you’re using an older Linux system, the `ifconfig` way you have
to do. If you’re on a newer system, never forget to use the new way `ip`
and `netplan`, it's really recommended for you.

## References

- [Network Configuration](https://ubuntu.com/server/docs/network-configuration)
- [How to Manually Set Your IP in Linux (including ip/netplan)](https://danielmiessler.com/study/manually-set-ip-linux/)
