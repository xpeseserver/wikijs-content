---
title: Docker
description: everything for docker
published: 1
date: 2022-01-20T08:48:18.734Z
tags: docker, server
editor: markdown
dateCreated: 2022-01-20T08:48:18.734Z
---

# Docker
Everything is stored at `/docker` and should be runnning witth `docker-compose`.
Also if a volume is linked with `./` you need to create it where the yml is located.
## Dashboard
```
version: "2.1"
services:
  heimdall:
    image: lscr.io/linuxserver/heimdall:latest
    container_name: heimdall
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Vienna
    volumes:
      - ./config:/config
    ports:
      - 3002:80
    restart: unless-stopped

```

## Filebrowser
```
version: '3'

services:
  filebrowser-web:
    image: filebrowser/filebrowser:latest
    ports:
      - "8080:80"
    volumes:
      - ./files:/srv
      - ./filebrowser.db:/database.db
      - ./settings.json:/.filebrowser.json
    restart: unless-stopped
```

### settings.json
```
{
  "port": 80,
  "baseURL": "",
  "address": "",
  "log": "stdout",
  "database": "/database.db",
  "root": "/srv"
}
```

## VPN
```
version: "2.1"
services:
  openvpn-as:
    image: ghcr.io/linuxserver/openvpn-as
    container_name: openvpn-as
    cap_add:
      - NET_ADMIN
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Vienna
      - INTERFACE=enp37s0 #optional
    volumes:
      - ./config:/config
    ports:
      - 943:943
      - 9443:9443
      - 1194:1194/udp
    restart: unless-stopped
```

## TS3 Bot
```
sinusbot:
  image: sinusbot/docker
  restart: unless-stopped
  ports:
    - 8087:8087
  volumes:
    - ./scripts:/opt/sinusbot/scripts
    - ./data:/opt/sinusbot/data
  environment:
    UID: 1015
    GID: 1015
    OVERRIDE_PASSWORD: #####
```

## Uptime
```
version: "3"
services:
  uptime-kuma:
    image: louislam/uptime-kuma:latest
    ports:
      - "3001:3001"
    volumes:
      - ./data:/app/data
    restart: unless-stopped
```

## Docker updater
```
version: "3"
services:
  watchtower:
    image: containrrr/watchtower:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    restart: unless-stopped
```

## Wiki
```
version: "2.1"
services:
  wikijs:
    image: linuxserver/wikijs
    container_name: wikijs
    environment:
      - PUID=1016
      - PGID=1017
      - TZ=Europe/Vienna
    volumes:
      - ./config:/config
      - ./data:/data
    ports:
      - 3000:3000
    restart: unless-stopped
```
