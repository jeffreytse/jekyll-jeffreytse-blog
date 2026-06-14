---
layout: post
title: 'A Story About Ctrl+C Under Terminal'
subtitle: 'What really happens from keypress to process death'
banner:
  image: https://i.postimg.cc/fLvY2Bdv/image.png
  opacity: 0.9
author: Jeffrey Tse
categories: computer
tags:
  - linux
  - terminal
  - note
---

## Introduction

You've done it a thousand times. A command hangs, a loop spins forever, a
program misbehaves — and you reach for `Ctrl+C`. The process dies. You move on.

But what exactly happened in that fraction of a second? It's not magic, and it's
not the operating system simply "killing" the program. There's a whole chain of
events that unfolds the moment your finger hits those two keys — one that
touches the kernel, process management, and Unix philosophy all at once.

This is that story.

## The Keystroke Journey

When you press `Ctrl+C`, the first stop is your **terminal emulator** (e.g.,
GNOME Terminal, iTerm2, xterm). The emulator reads the raw key event and
writes the byte `0x03` (ASCII ETX — "End of Text") into the **PTY master**
(pseudo-terminal master).

The kernel's **TTY line discipline** sits on the other side of that PTY. It
reads the incoming bytes and checks: is this byte the configured _interrupt
character_? By default, it is.

You can inspect and modify this with `stty`:

```bash
stty -a | grep intr
# speed 38400 baud; ...
# intr = ^C; quit = ^\; erase = ^?; kill = ^U; ...
```

`intr = ^C` means: when the line discipline sees byte `0x03`, treat it as an
interrupt. You can remap it:

```bash
stty intr ^X   # Ctrl+X becomes the interrupt key
```

The line discipline does **not** pass `^C` through to the program's stdin.
Instead, it triggers a signal.

## SIGINT: The Signal

The line discipline delivers **SIGINT** (signal number 2) to the process. The
name stands for _Signal Interrupt_ — historically the signal sent when you
interrupt a program from the keyboard.

SIGINT's default behavior is to **terminate the process**. But unlike SIGKILL,
it can be caught or ignored by the program — which is why some programs handle
it gracefully (cleanup, save state) before exiting.

Here's a quick reference for the terminal control signals:

| Shortcut  | Signal   | Number | Default Action        | Catchable? |
| --------- | -------- | ------ | --------------------- | ---------- |
| `Ctrl+C`  | SIGINT   | 2      | Terminate             | Yes        |
| `Ctrl+Z`  | SIGTSTP  | 20     | Suspend (stop)        | Yes        |
| `Ctrl+\`  | SIGQUIT  | 3      | Terminate + core dump | Yes        |
| `kill -9` | SIGKILL  | 9      | Terminate (forceful)  | **No**     |
| `Ctrl+D`  | _(none)_ | —      | EOF on stdin          | N/A        |

Note that `Ctrl+D` is not a signal at all — it flushes the input buffer and
sends EOF, which programs may interpret as "no more input."

## Process Groups — Why the Whole Pipeline Dies

Here's where it gets interesting. SIGINT is not sent to a single PID. It's sent
to the **foreground process group**.

When you run a pipeline:

```bash
cat /dev/urandom | tr -dc 'a-z' | head -c 100
```

The shell places all three processes (`cat`, `tr`, `head`) into the same process
group. The terminal tracks which process group is in the "foreground." When you
press `Ctrl+C`, the kernel sends SIGINT to every process in that group
simultaneously.

You can verify this with:

```bash
# In another terminal while the pipeline runs:
ps -o pid,pgid,comm | grep -E 'cat|tr|head'
#  PID  PGID COMMAND
# 1234  1234 cat
# 1235  1234 tr
# 1236  1234 head
```

All three share the same PGID. Ctrl+C kills all three — not just the last in the
chain.

## Catching and Ignoring Signals

Because SIGINT is catchable, programs can intercept it and decide what to do.

**In Bash:**

```bash
trap 'echo "Caught Ctrl+C, cleaning up..."; exit 1' INT

while true; do
  echo "working..."
  sleep 1
done
```

Now `Ctrl+C` runs your cleanup before exiting.

**In Python:**

```python
import signal
import sys

def handler(sig, frame):
    print("\nCaught SIGINT, exiting cleanly.")
    sys.exit(0)

signal.signal(signal.SIGINT, handler)

# Or simply catch the exception:
try:
    while True:
        pass
except KeyboardInterrupt:
    print("Interrupted!")
```

Python maps SIGINT to the `KeyboardInterrupt` exception, so you can handle it in
a `try/except` block without touching the `signal` module at all.

To **ignore** SIGINT entirely:

```bash
signal(SIGINT, SIG_IGN)   # C
trap '' INT               # Bash
```

## Detaching from the Terminal

If you want a process to survive even when the terminal closes (which sends
SIGHUP), use `nohup`:

```bash
nohup long_running_command &
```

`nohup` sets SIGHUP to be ignored and redirects output to `nohup.out`. The
process won't receive `Ctrl+C` either, since it's in the background.

`disown` removes an already-running background job from the shell's job table so
it won't receive SIGHUP when the shell exits:

```bash
long_running_command &
disown %1
```

## Edge Cases

**SSH sessions:** When you press `Ctrl+C` in an SSH session, the SSH client
detects it and sends a channel request to the SSH server, which delivers SIGINT
to the remote process. It works the same way — but the signal travels over the
network.

**Docker containers:** If you run a container without `-it`, the container's
init process doesn't have a proper TTY. `Ctrl+C` may not reach the container
process at all. Always use:

```bash
docker run -it myimage   # allocates a pseudo-TTY
```

**Background processes:** A process started with `&` has SIGINT set to _ignored_
by the shell. It won't be killed by `Ctrl+C` from the terminal — you'd need to
`kill` it explicitly.

## Why Ctrl+C Sometimes Doesn't Work

Two common reasons:

1. **The process is catching SIGINT.** It has a handler and hasn't exited yet.
   Try `Ctrl+\` (SIGQUIT) which also produces a core dump, or send SIGTERM
   first, then SIGKILL.

2. **The process is in uninterruptible sleep (state `D`).** This happens during
   certain kernel I/O waits (e.g., NFS hangs, disk I/O). In state `D`, the
   process cannot be killed by _any_ signal — not even SIGKILL. The kernel has
   to complete or time out the I/O first.

Check process state:

```bash
ps aux | awk '$8 == "D" {print}'
```

If a process is stuck in `D`, only fixing the underlying I/O issue (remount,
disconnect NFS share, reboot) will resolve it.

## Summary

To summarize what happens in that fraction of a second when you press `Ctrl+C`:

1. Terminal emulator writes byte `0x03` to PTY master
2. Kernel TTY line discipline recognizes it as the interrupt character
3. Line discipline sends **SIGINT** to the **foreground process group**
4. Every process in the group receives SIGINT simultaneously
5. Processes with no handler terminate immediately
6. Processes with a handler run cleanup logic before (optionally) exiting

That's the full story of `Ctrl+C` — from keypress to process death.
