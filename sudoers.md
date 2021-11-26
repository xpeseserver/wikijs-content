---
title: sudoers
description: Allow to use sudo without password
published: 1
date: 2021-11-26T12:13:59.422Z
tags: sudo, admin
editor: markdown
dateCreated: 2021-11-26T12:13:59.422Z
---

# How to edit the sudoers
`sudo visudo`
## Allow users
`<username> ALL=(ALL) NOPASSWD:ALL`

## Allow files 
`<username> ALL=(ALL) NOPASSWD: /path/to/script`