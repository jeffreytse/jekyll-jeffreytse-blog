---
layout: post
title: How to use fcitx5 elegantly on Arch Linux
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - linux
  - misc
---

## Introduction

Fcitx [ˈfaɪtɪks] is an input method framework with extension support.
Currently it supports Linux and Unix systems like freebsd. It has
three built-in Input Method Engine, Pinyin, QuWei and Table-based
input methods.

Fcitx tries to provide a native feeling under all desktop as well as
a light weight core. You can easily customize it to fit your
requirements.

Compared with fcitx4, the experience has improved significantly, and
many practical functions have been added.

Here are some stuffs worth mentioning:

- The input is much smoother and almost no bugs.
- Support [Wayland](https://en.wikipedia.org/wiki/Wayland_display_server_protocol)
  communication protocol.
- Generate word candidates based on prefix automatically ([See here](https://github.com/felixonmars/fcitx5-pinyin-zhwiki/issues/6)).
- The U-mode for inputting Chinese character in splitting.
- Compatible with input method modules of `fcitx` and `ibus`.
- Support Baidu cloud vocabulary and Sogou cell vocabulary.
- The only disadvantage is that there are few themes.

Fcitx5 has been developed for more than three years, and it has been
well received by many Archers, so why not upgrade your fcitx4 to fcitx5.

## Installation

```bash
# Remove fcitx4
pacman -Rs $(pacman -Qsq fcitx)

# Install fcitx5 from community source
pacman -S fcitx5 fcitx5-gtk fcitx5-qt

# Install configuration tool
pacman -S fcitx5-configtool
```

Below packages are optional:

```bash
# Install Chinese addons (Cloud Pinyin, Simplified Chinese)
pacman -S fcitx5-chinese-addons

# Install Rime if you better like it (Traditional/Simplified Chinese)
pacman -S fcitx5-rime

# Install Japanese IM
pacman -S fcitx5-anthy

# Install Japanese IM using Google Engine
pacman -S fcitx5-mozc
```

## Configuration

### Default Profile

Fcitx5 uses the Western keyboard by default, for other input methods like
pinyin, you should modify the default profile.

Especially, because fcitx5 will automatically overwrite the profile
configuration file when exiting, **PLEASE DO NOT FORGET TO CLOSE** fcitx5
process before you start to modify the profile file.

Edit `~/.config/fcitx5/profile`

```ini
############################################
# DefaultIM settings
#
# 1. Pinyin is for Chinese (supported by `fcitx5-chinese-addons`)
# DefaultIM=pinyin
#
# 2. Rime is for Chinese (supported by `fcitx5-rime`)
# DefaultIM=rime
#

[Groups/0]
# Group Name
Name=Default
# Layout
Default Layout=us
# Default Input Method
DefaultIM=pinyin

[Groups/0/Items/0]
# Name
Name=keyboard-us
# Layout
Layout=

[Groups/0/Items/1]
# Name
Name=pinyin
# Layout
Layout=

[GroupOrder]
0=Default
```

### Environment Variables

At first, get your X Desktop Environment Type:

```bash
echo ${XDG_SESSION_TYPE}
```

Then edit `~/.pam_environment` (for **X11** and **Waylanda** users)

```bash
GTK_IM_MODULE=fcitx5
QT_IM_MODULE=fcitx5
XMODIFIERS="@im=fcitx5"
```

or edit `~/.xprofile` (only for **X11** users)

```bash
# export fcitx5 environment variables
export GTK_IM_MODULE=fcitx5
export QT_IM_MODULE=fcitx5
export XMODIFIERS="@im=fcitx5"
```

Additionally, the file `~/.bash_profile` or `~/.profile` also can
be used for exporting the environment variables, but the SDDM will
only load `.bash_profile` when both configuration files exist at
the same time.

### Autostart

If you are a KDE desktop user, you can easily add autostart item
on **System Settings** as below:

![image](https://user-images.githubusercontent.com/9413601/100999815-1fd0a280-3598-11eb-9cf3-e77d31d2198a.png)

or if you are a terminal user and better like termination way, you just
need to create and edit `~/.config/autostart/fcitx5.desktop`:

```ini
[Desktop Entry]
Name=Fcitx5
GenericName=Fcitx5 Input Method
Comment=Start Fcitx5
Exec=fcitx5
Icon=fcitx
Terminal=false
Type=Application
Categories=System;Utility;
StartupNotify=false
X-GNOME-Autostart-Phase=Applications
X-GNOME-AutoRestart=false
X-GNOME-Autostart-Notify=false
X-KDE-autostart-after=panel
X-KDE-StartupNotify=false
X-GNOME-Autostart-enabled=true

```

or even You can directly add to `~/.xprofile`:

```bash
fcitx5 &
```

### Theme

If you don’t like the default theme that comes with it, you can also
try to install a new theme, here is a example for demonstration:

![image](https://user-images.githubusercontent.com/9413601/101030668-59170b80-35b4-11eb-8a0c-3867ec9138c5.png)

Firstly, install the material style theme package:

```bash
# Material Style Theme
# https://github.com/hosxy/Fcitx5-Material-Color
pacman -S fcitx5-material-color
```

then edit `~/.config/fcitx5/conf/classicui.conf` file:

```ini
# We choose one theme, such as `Pink`, 'Blue', 'Black', etc.
Theme=Material-Color-Pink
```

### Other

#### Disable Cloud Pinyin

To prevent privacy from being uploaded, you can disable the Cloud
Pinyin.

Edit `~/.config/fcitx5/conf/pinyin.conf`:

```ini
# Enable/Disable Cloud Pinyin
CloudPinyinEnabled=False
```

#### Disable Auto DPI

By default, fcitx5 can automatically adjust the UI size according to
the DPI of the display, but sometimes it will be wrong. You can set
to a fixed font size.

Edit `~/.config/fcitx5/conf/classicui.conf`:

```ini
# Enable/Disable auto DPI
PerScreenDPI=False

# Font (Here you can set to any font you like)
Font="Noto Sans Regular 14"
```

#### Enable Inline Preedit

If you want it to display pre-edited text in the app when available,
here you must not miss it. You should create or edit specific
configuration file for different IMs:

- Pinyin IM: `~/.config/fcitx5/conf/pinyin.conf`.
- Rime IM: `~/.config/fcitx5/conf/rime.conf`.

```ini
# Display pre-edited text in the app when available
PreeditInApplication=True
```

#### Customize Quick Phrase

At First, create a quick phrase database:

```bash
sudo touch /usr/share/fcitx5/data/quickphrase.d/quick.mb
```

And then append all the quick phrases line by line with the format
`input output` to the file:

```txt
eg e.g
asap as soon as possible
omg Oh my god!
...
```

You can open the Quick Input by pressing down the semicolon, but
unfortunately, Rime does not support it.

## Conclusion

In general, the input experience of fcitx5 is indeed better than
the previous version. The input is relatively smooth. You can input
the Chinese semicolon through pressing the semicolon twice. Also, it
will automatically switch to half-width punctuation when inputting
English.

## References

- [Fcitx Official Site](https://fcitx-im.org/wiki/Fcitx)
- [How to use Fcitx5 on Arch Linux now](https://www.csslayer.info/wordpress/fcitx-dev/%e5%a6%82%e4%bd%95%e7%8e%b0%e5%9c%a8%e5%b0%b1%e5%9c%a8-arch-linux-%e7%94%a8%e4%b8%8a-fcitx-5/#comment-28741)
