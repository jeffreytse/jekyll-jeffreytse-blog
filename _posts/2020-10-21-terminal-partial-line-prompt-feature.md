---
layout: post
title: Terminal partial line prompt feature
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - terminal
---

## 1. Introduction

If you are a user who often deals with terminals, you must have noticed
that the output ends a line with a highlighted percent symbol on occasion
with a variety of applications. Maybe you would think it was because the
output was cancelled early (ctrl+c, for example) or something similar,
but it doesn't seem to do this in bash, just do in zsh/fish.

## 2. Learn more about

This happens because it is a "partial line". The specific feature of zsh
(and now fish as well) to let you clearly see unterminated lines in a
command's output. And by default [zsh goes to the next line to avoid
covering it with the prompt](http://zsh.sourceforge.net/Doc/Release/Options.html#Prompting).

> When a partial line is preserved, by default you will see an
> inverse+bold character at the end of the partial line: a "%" for
> a normal user or a "#" for root. If set, the shell parameter
> PROMPT_EOL_MARK can be used to customize how the end of partial
> lines are shown.

In traditional shells (e.g. sh/bash), if a command outputs some data
after the last newline character, or, in other words, if it leaves the
terminal cursor not at the start of the line, the next prompt by the
shell ends up appended to that last unterminated line.

Let's do the test by using the following commands in zsh and bash
respectively:

```zsh
$ echo -n -e "This is a partial line."
```

```zsh
$ echo -n -e "This is a partial line.\n"
```

The `echo` program options:

- `-n` - Do not output the trailing newline
- `-e` - Enable interpretation of backslash escapes
- `-E` - Disable interpretation of backslash escapes (default)

You will see below result:

![image](https://user-images.githubusercontent.com/9413601/96744023-2d223b00-13f7-11eb-9ba1-31985f3648b5.png)

## References

- [Why does a cURL request return a percent sign (%) with every request in ZSH?](https://stackoverflow.com/questions/29497038/why-does-a-curl-request-return-a-percent-sign-with-every-request-in-zsh)
- [Why ZSH ends a line with a highlighted percent symbol?](https://unix.stackexchange.com/questions/167582/why-zsh-ends-a-line-with-a-highlighted-percent-symbol)
