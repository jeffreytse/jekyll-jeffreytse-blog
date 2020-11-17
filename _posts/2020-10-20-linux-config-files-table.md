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

| Path                      | Type   | Scope  | Description                            |
| ------------------------- | ------ | ------ | -------------------------------------- |
| /etc/locale.conf          | File   | Global | Global locale                          |
| /etc/security/limits.conf | File   | Global | Global limits for a user               |
| /etc/environment          | File   | Global | Global enviroment variables            |
| /etc/profile              | File   | Global | Global profile                         |
| /etc/profile.d            | Folder | Global | Global profiles                        |
| /etc/default              | Folder | Global | Global defaults(e.g. keyboard, locale) |
| ~/.profile                | File   | User   | User profile                           |
| ~/.bash_profile           | File   | User   | User profile                           |
| ~/.bash_login             | File   | User   | User profile                           |
| ~/.bashrc                 | File   | User   | User bash resources                    |
| ~/.xinitrc                | File   | User   | User resources on X server environment |

## References

https://help.ubuntu.com/community/EnvironmentVariables

https://askubuntu.com/questions/866161/setting-path-variable-in-etc-environment-vs-profile
