---
layout: post
title: How to change startup programs manually in macOS
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - macos
  - note
---

| Path                          | Type   | Scope    | Description                      |
| ----------------------------- | ------ | -------- | -------------------------------- |
| ~/Library/Preferences         | Folder | One User | Launch items under LoginHook key |
| ~/Library/LaunchAgents        | Folder | One User | Launch agents for one user       |
| /Library/StartUpItems         | Folder | Any User | Start up items for any user      |
| /Library/LaunchDaemons        | Folder | Any User | Launch daemons for any user      |
| /Library/LaunchAgents         | Folder | Any User | Launch agents for any user       |
| /System/Library/LaunchDaemons | Folder | System   | System level of launch daemons   |
| /System/Library/LaunchAgents  | Folder | System   | System level of launch agents    |
