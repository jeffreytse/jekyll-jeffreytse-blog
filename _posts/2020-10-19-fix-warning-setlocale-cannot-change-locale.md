---
layout: post
title: Fix warning setlocale cannot change locale
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - terminal
  - misc
---

## 1. Introduction

When you are using the terminal and encounter the following warning
promtp like `warning: setlocale: LC_ALL: cannot change locale (en_US.UTF-8)`,
you can not figure it out and you are most likely confused, this
article would help you solve this problem.

## 2. Solution

```bash
$ sudo locale
```

Edit the configuration file for `locale-gen`:

```bash
$ sudo vim /etc/locale.gen
```

> This file lists locales that you wish to have built. You can find a list
> of valid supported locales at /usr/share/i18n/SUPPORTED, and you can add
> user defined locales to /usr/local/share/i18n/SUPPORTED. If you change
> this file, you need to rerun locale-gen.

Add or uncomment the locale `en_US.UTF-8 UTF-8` and rerun `locale-gen`:

```bash
$ sudo locale-gen
```

## 3. Conclusion

This error happens when your terminal settings local locale environment
variables which doesn’t have the specific locale you requested, to solve
this problem you should configure and generate the locales.
