---
layout: post
title: Fix invalid or corrupted package in Arch Linux
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - misc
---

## What's up?

Recently, when I use `yay -Syu` to update the software packages, it always
prompts that a package cannot be updated and prompts are `warning: could not fully load metadata for package` and `error: failded to prepare transaction (invalid or corrupted package)`. It's time to solve this annoying problem.

![image](https://user-images.githubusercontent.com/9413601/95043413-3f218f80-070f-11eb-8491-ee15fad77608.png)

## Remove first

Try to remove it first:

```bash
$ yay -Rdd zoom
```

It still cannot be removed mannually and this time the prompt becomes `error: could not remove database entry`.

![image](https://user-images.githubusercontent.com/9413601/95043599-d8e93c80-070f-11eb-8625-dc7fc073dd94.png)

## Reinstall with the verbose option

And then try to reinstall it with verbose option:

```bash
$ yay -Sv zoom
```

This time the problem remains, but we got the verbose:

![image](https://user-images.githubusercontent.com/9413601/95043488-742de200-070f-11eb-9605-3dd8392c75f0.png)

## Analyze the problem

According to the prompts, we know that this issue is related to metadata of
the package. And since the metadata is stored in Database, so we check the
DB data by the **DB Path** in the verbose.

### Explore the structure

List the DB directory:

```bash
$ ls -la /var/lib/pacman/
```

![image](https://user-images.githubusercontent.com/9413601/95051588-105fe500-0720-11eb-83a8-189fde1a6cff.png)

There are two folders:

- local (for local packages data)
- sync (for sync data)

List the `local` directory:

```bash
$ ls -la /var/lib/pacman/local
```

![image](https://user-images.githubusercontent.com/9413601/95052781-1bb41000-0722-11eb-95f0-e80ebc74dd2d.png)

List the `sync` directory:

```bash
$ ls -la /var/lib/pacman/sync
```

![image](https://user-images.githubusercontent.com/9413601/95051609-19e94d00-0720-11eb-9617-b0d90d441d18.png)

### Compare the structure

List the invalid package directory:

```bash
$ ls -la /var/lib/pacman/local/zoom-2.9.265650.0716-1/
```

![image](https://user-images.githubusercontent.com/9413601/95043829-7c3a5180-0710-11eb-84c0-6a8753fc5e50.png)

List a local valid package directory:

```bash
$ ls -la /var/lib/pacman/local/git-2.28.0-1
```

![image](https://user-images.githubusercontent.com/9413601/95044004-f23eb880-0710-11eb-8c05-327d61502b33.png)

We can find that compared with the normal package, the invalid package
lacks some directories and files. It is not difficult to figure out that
it is this missing that caused removal or update to be abnormal.

## Fix the problem

Therefore, we remove the invalid package data mannually:

```bash
$ sudo rm -rf /var/lib/pacman/local/zoom-2.9.265650.0716-1/
```

And then we install the package again:

```bash
$ yay -S zoom
```

Wow! Now the package can be installed without any error prompts.

![image](https://user-images.githubusercontent.com/9413601/95043660-0504bd80-0710-11eb-8a74-64db4d2e4937.png)
