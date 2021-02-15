---
layout: post
title: Linux config files table
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - misc
---

## Table

| Path                       | Type   | Scope  | Description                            |
| -------------------------- | ------ | ------ | -------------------------------------- |
| /etc/locale.conf           | File   | Global | Global locale                          |
| /etc/security/limits.conf  | File   | Global | Global limits for a user               |
| /etc/environment           | File   | Global | Global enviroment variables            |
| /etc/login.defs            | File   | Global | Global login-related settings          |
| /etc/profile               | File   | Global | Global profile                         |
| /etc/profile.d             | Folder | Global | Global profiles                        |
| /etc/default               | Folder | Global | Global defaults(e.g. keyboard, locale) |
| /etc/bash.bashrc           | File   | Global | Global bash configuration              |
| /etc/security/pam_env.conf | File   | Global | Global enviroment variables            |
| ~/.pam_environment         | File   | User   | User enviroment variables              |
| ~/.profile                 | File   | User   | User profile                           |
| ~/.bash_profile            | File   | User   | User profile on bash                   |
| ~/.bash_login              | File   | User   | User configuration on bash login       |
| ~/.bash_logout             | File   | User   | User configuration on bash logout      |
| ~/.bashrc                  | File   | User   | User bash resources                    |
| ~/.xinitrc                 | File   | User   | User resources on X server environment |
| ~/.xprofile                | File   | User   | User profile on X server environment   |
| ~/.xsession                | File   | User   | User session on X server environment   |
| ~/.inputrc                 | File   | User   | User readline's configuration          |

support for `~/.pam_environment` is removed. ([See here](https://github.com/linux-pam/linux-pam/blob/62d826471e87e27b39a36ccbeee58999e2514a92/NEWS#L29))

## References

- [EnvironmentVariables](https://help.ubuntu.com/community/EnvironmentVariables)
- [Setting PATH variable in /etc/environment vs .profile](https://askubuntu.com/questions/866161/setting-path-variable-in-etc-environment-vs-profile)
