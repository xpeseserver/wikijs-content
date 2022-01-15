---
title: Nginx-proxy
description: SSL and subdomain ur containers
published: 1
date: 2022-01-15T12:26:20.341Z
tags: web, https, proxy, nginx, ssl
editor: markdown
dateCreated: 2022-01-15T12:26:20.341Z
---

# Nginx-Proxy
## docker-compose.yml
```yaml:
version: '2'
services:
  nginx-proxy:
    image: jwilder/nginx-proxy:alpine
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro
      - conf:/etc/nginx/conf.d
      - certs:/etc/nginx/certs:ro
      - vhost:/etc/nginx/vhost.d
      - html:/usr/share/nginx/html
    network_mode: bridge

  nginx-proxy-letsencrypt-ssl:latest
    image: nginxproxy/acme-companion
    container_name: nginx-proxy-acme
    volumes_from:
      - nginx-proxy
    volumes:
      - certs:/etc/nginx/certs:rw
      - acme:/etc/acme.sh
      - /var/run/docker.sock:/var/run/docker.sock:ro
    network_mode: bridge

volumes:
  conf:
  vhost:
  html:
  certs:
  acme:
  ```
  ## Container config
  TBD