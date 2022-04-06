---
layout: post
title: Understanding of Shell initialization process
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - terminal
---

For Bash reads .bashrc file in non login interactive shell and `.bash_profile` in login shells.

Zsh reads .zshrc in an interactive shell and .zprofile in a login shell.

## Interactive Shell and Login Shell

Interactive shell is a simple shell that drives input from the user and returns the desired output.

A login shell is the first process that executes under our user ID when we log in to a session.

- `~/.bash_profile` for bash login shell
- `~/.bash_login` derived from the C shell’s file named `.login`
- `~/.profile` derived from the Bourne shell and Korn shell files named `.profile`

```txt
+----------------+--------+-----------+---------------+
|                | login  |interactive|non-interactive|
|                |        |non-login  |non-login      |
+----------------+--------+-----------+---------------+
|/etc/profile    |   A    |           |               |
+----------------+--------+-----------+---------------+
|/etc/bash.bashrc|        |    A      |               |
+----------------+--------+-----------+---------------+
|~/.bashrc       |        |    B      |               |
+----------------+--------+-----------+---------------+
|~/.bash_profile |   B1   |           |               |
+----------------+--------+-----------+---------------+
|~/.bash_login   |   B2   |           |               |
+----------------+--------+-----------+---------------+
|~/.profile      |   B3   |           |               |
+----------------+--------+-----------+---------------+
|BASH_ENV        |        |           |       A       |
+----------------+--------+-----------+---------------+
```

Fish is not a POSIX 1003.1 compatible shell

## References

- http://feihu.me/blog/2014/env-problem-when-ssh-executing-command-on-remote/
- https://dev.to/jasmin/a-brief-difference-between-zsh-and-bash-5ebp#:~:text=Bash%20sets%20the%20prompt%20from,ways%20to%20do%20fancy%20customizations.
- https://www.linuxquestions.org/questions/programming-9/how-to-check-in-a-script-whether-the-shell-is-login-or-non-login-360629/
- https://github.com/fish-shell/fish-shell/issues/3665
- https://zhuanlan.zhihu.com/p/47819029
- https://joshstaiger.org/archives/2005/07/bash_profile_vs.html
