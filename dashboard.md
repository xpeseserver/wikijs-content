---
title: Landingpage
description: Gameserver dashboard
published: 1
date: 2021-11-26T12:19:57.759Z
tags: php, web
editor: markdown
dateCreated: 2021-11-26T12:15:06.475Z
---

# Nginx
## User
`www-data`
## scripts

`sudo chmod 755 /var/www/scripts/*`
`sudo chown -R root:root /var/www/scripts/*`

### Allow execute with sudo
`sudo visudo`
Content:
`www-data ALL=(root) NOPASSWD: /var/www/scripts/restart.sh`
`www-data ALL=(root) NOPASSWD: /var/www/scripts/start.sh`
`www-data ALL=(root) NOPASSWD: /var/www/scripts/stop.sh`
`www-data ALL=(root) NOPASSWD: /var/www/scripts/details.sh`
`www-data ALL=(root) NOPASSWD: /var/www/scripts/update.sh`