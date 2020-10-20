---
layout: post
title: Fix errors occurred no packages were upgraded in Arch Linux
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - misc
---

## 1. What's up?

When you use `yay -S <package>` to install some package and face this
prompt `errors occured, no packages were upgraded`, don't worry, this
article will guide you to settle it down.

## 2. Problem reproduce

At First, let's try to remove any local package(e.g. zoom) mannually:

```bash
$ sudo rm -rf /var/lib/pacman/local/zoom-2.9.265650.0716-1/
```

And then we install this package again:

```bash
$ yay -S zoom
```

Look! We reproduced this problem as below:

![image](https://user-images.githubusercontent.com/9413601/95348585-c548fc00-08f0-11eb-9d55-55b943426eec.png)

## 3. Fix the problem

Since we only partially removed the package metadata files, the package
is inconsistent with the database, so that the package was corrupted.

Therefore, we should install the package with overwrite option:

```bash
$ yay -S zoom --overwrite '*'
```

or

```bash
$ yay -S zoom --dbonly
```

Congratulations! Now the package can be installed without any error prompts.

![image](https://user-images.githubusercontent.com/9413601/95345539-67ff7b80-08ed-11eb-86ef-e29754dd69e2.png)
