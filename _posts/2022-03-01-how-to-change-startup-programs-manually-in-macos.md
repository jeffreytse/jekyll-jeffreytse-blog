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

There are some configuration folders for startup item in macOS.

| Path                          | Type   | Scope     | Description                                     |
| ----------------------------- | ------ | --------- | ----------------------------------------------- |
| ~/Library/Preferences         | Folder | One User  | Launch items under LoginHook key                |
| ~/Library/LaunchAgents        | Folder | One User  | Launch agents for a specific user               |
| /Library/StartUpItems         | Folder | All Users | Start up items for all users                    |
| /Library/LaunchDaemons        | Folder | All Users | Launch daemons for installed third-party apps   |
| /Library/LaunchAgents         | Folder | Any Users | Launch agents for all users                     |
| /System/Library/LaunchDaemons | Folder | System    | Launch daemons for native macOS processes       |
| /System/Library/LaunchAgents  | Folder | System    | Launch agents managed by macOS since OS X 10.11 |

We can also manage a service of different domains by `launchctl` commands.

```bash
# List information about services
launchctl list

# Tears down a domain or removes a service from a domain
launchctl bootout gui/501/Users/username/Library/LaunchAgents/com.google.keystone.agent.plist
```
