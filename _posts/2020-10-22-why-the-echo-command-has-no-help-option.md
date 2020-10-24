---
layout: post
title: Why the echo command has no help option?
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - terminal
---

## 1. Introduction

Have you ever tried to use the `echo --help` command to get some
help, but it just simply prints '--help' literally, and similarly,
that `echo --version` has the same result. Why it didn't work,
this article will lead us to find out more information.

## 2. Learn more about

This happens because you are using [the `echo` built-in command of
bash](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#index-echo),
which does not understand the `--help` option. The GNU `echo`
supports a `--help` option, as do some others. We could use
`man echo` command that relates to [the linux man page of echo program](https://linux.die.net/man/1/echo).

To access the echo program, rather than the builtin, you can either
give a path to it:

```bash
$ /bin/echo --help
```

or use Bash's [`enable` command](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html#index-enable) to disable the built-in version:

```bash
$ enable -n echo
$ echo --help
```

Therefore, we can try it as below:

![image](https://user-images.githubusercontent.com/9413601/96819868-422eb680-1457-11eb-9558-c84535f43335.png)

## References

- [why 'echo --help' doesn't give me help page of echo?](https://unix.stackexchange.com/questions/153660/why-echo-help-doesnt-give-me-help-page-of-echo)
