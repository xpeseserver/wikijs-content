---
title: Game-Dashboard
description: Gameserver dashboard
published: 1
date: 2022-01-20T07:41:43.504Z
tags: php, web
editor: markdown
dateCreated: 2021-11-26T12:15:06.475Z
---

# Caddy
## User
`caddy`
## scripts

`sudo chmod 755 /var/www/scripts/*`
`sudo chown -R root:root /var/www/scripts/*`

### Allow script execute with sudo
`sudo visudo`
Content:
`caddy ALL=(root) NOPASSWD: /var/www/scripts/restart.sh`
`caddy ALL=(root) NOPASSWD: /var/www/scripts/start.sh`
`caddy ALL=(root) NOPASSWD: /var/www/scripts/stop.sh`
`caddy ALL=(root) NOPASSWD: /var/www/scripts/details.sh`
`caddy ALL=(root) NOPASSWD: /var/www/scripts/update.sh`