---
layout: post
title: Accessing an SMB Share with Linux Machines
author: Jeffrey Tse
banner: https://bit.ly/3iHyE1P
categories: computer
tags:
  - computer
  - linux
  - terminal
---

Linux (UNIX) machines can also browse and mount SMB shares. Note that this can
be done whether the server is a Windows machine or a Samba server! I boil down
the essentials in an easy-to-follow post.

## The difference between CIFS and SMB

SMB stands for "Server Message Block". It's a file sharing protocol that was
invented by IBM and has been around since the mid-eighties. Since it's a
protocol (an agreed upon way of communicating between systems) and not a
particular software application, if you're troubleshooting, you're looking for
the application that is said to implement the SMB protocol.

The SMB protocol was designed to allow computers to read and write files to a
remote host over a local area network (LAN). The directories on the remote
hosts made available via SMB are called "shares".

CIFS stands for "Common Internet File System". CIFS is a dialect of SMB. That
is, CIFS is a particular implementation of the SMB protocol, created by Microsoft.

Most people, when they use either SMB or CIFS, are talking about the same exact
thing. But if they’re essentially the same thing, why should I always use SMB?

Two reasons:

- The CIFS implementation of SMB is rarely used these days. Under the covers,
  most modern storage systems no longer use CIFS, they use SMB 2 or SMB 3. In
  the Windows world, SMB 2 has been the standard as of Windows Vista (2006)
  and SMB 3 is part of Windows 8 and Windows Server 2012.

- CIFS has a negative connotation amongst pedants. SMB 2 and SMB 3 are massive
  upgrades over the CIFS dialect, and storage architects who are near and dear
  to file sharing protocols [don’t appreciate the misnomer](http://blog.fosketts.net/2012/02/16/cifs-smb/).
  It’s kind of like calling an executive assistant a secretary.

## The ways to access an SMB Share

The easiest and most reliable way to share files between a Linux and Windows
computer on the same local area network is to use the Samba file sharing
protocol. All modern versions of Windows come with Samba installed, and
Samba is installed by default on most distributions of Linux. So I wrote some
ways to help you access an SMB share conveniently.

### An SMB client program

An SMB client program for UNIX machines is included with the Samba distribution.
It provides an ftp-like interface on the command line. You can use this utility
to transfer files between a Windows 'server' and a Linux client.

To see which shares are available on a given host, run:

```bash
$ smbclient -L server
```

The browse list shows other SMB servers with resources to share on the network,
run:

```bash
$ smbcient //server/share <password>
```

If you can use ftp, you shouldn't need the man pages for `smbclient`.

### Mount/Umount with smbfs package

Although you can use `smbclient` for testing, you will soon tire of it for real
work. For that you will probably want to use the smbfs package.

Most Linux distributions also now include the useful smbfs package, which comes
with two simple utilities, `smbmount` and `smbumount`.


The following shows a typical use of `smbmount` to mount an SMB share:

```bash
$ smbmount "//server/share" -U rtg2t -c 'mount /share -u <uid> -g <gid>'
```

Please see the [manual](https://linux.die.net/man/8/smbmount) pages for
`smbmount` and `smbumount` for details on the above operation.

### Mount/Umount with uniformed way

Nowadays, `smbmount` has been deprecated in favor of `mount.cifs`, since at
least 2008. You might also need to install the cifs-utils package.

```bash
$ mount -t cifs //server/share/ /mnt/remote -o user=<username>,pass=<password>,uid=<username>,gid=<group>,noauto,user
```

Here's the accompanying [manpage](http://manpages.ubuntu.com/manpages/precise/en/man8/smbmount.8.html),
you would use these parameters instead.

### Use GUI file manager with smb protocol address

Since most default GUI file managers on Linux system support to browse the
filesystem based on SMB protocol, you can connect to a server by opening the
application on your Linux system.

Some file managers:

- Ubuntu/Debian: Nautilus (or `alt+F2`).
- Manjaro: Dolphin
- ...

Type `smb://server/share` on the address bar and stroke `Enter`.

## References

- [Accessing an SMB Share with Linux Machines](https://tldp.org/HOWTO/SMB-HOWTO-8.html)
- [CIFS vs SMB: What’s the Difference?](https://www.varonis.com/blog/cifs-vs-smb/)
