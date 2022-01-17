---
title: Nginx-proxy
description: SSL and subdomain ur containers
published: 1
date: 2022-01-17T08:27:34.036Z
tags: https, nginx, proxy, ssl, web
editor: markdown
dateCreated: 2022-01-15T12:26:20.341Z
---

# Nginx-Proxy
## docker-compose.yml
https://gist.github.com/w33ble/ab51b77641e499968c354ca02e4bccf0

1. mkdir vhost
2. curl -o templates/nginx.tmpl https://raw.githubusercontent.com/jwilder/nginx-proxy/master/nginx.tmpl

```yaml:
version: '3'

services:
  nginx-proxy:
    image: nginx:alpine
    container_name: proxy-nginx
    environment:
      - DEFAULT_HOST=xpese.spdns.de
    ports:
      - 80:80
      - 443:443
    volumes:
      - conf:/etc/nginx/conf.d:ro
      - ./vhost:/etc/nginx/vhost.d:ro
      - html:/usr/share/nginx/html:ro
      - certs:/etc/nginx/certs:ro

  dockergen:
    image: jwilder/docker-gen
    container_name: proxy-dockergen
    command: -notify-sighup proxy-nginx -wait 5s:30s -watch /etc/docker-gen/templates/nginx.tmpl /etc/nginx/conf.d/default.conf
    volumes:
      - /var/run/docker.sock:/tmp/docker.sock:ro
      - ./templates:/etc/docker-gen/templates:rw
      - conf:/etc/nginx/conf.d
      - ./vhost:/etc/nginx/vhost.d:ro
      - html:/usr/share/nginx/html
      - certs:/etc/nginx/certs:ro
    environment:
      - DEFAULT_HOST=xpese.spdns.de

  letsencrypt:
    image: jrcs/letsencrypt-nginx-proxy-companion
    container_name: proxy-letsencrypt
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./templates:/etc/docker-gen/templates:ro
      - conf:/etc/nginx/conf.d
      - ./vhost:/etc/nginx/vhost.d
      - html:/usr/share/nginx/html
      - certs:/etc/nginx/certs
    environment:
      - DEFAULT_EMAIL=xpeseserver@gmail.com
      - NGINX_PROXY_CONTAINER=proxy-nginx
      - NGINX_DOCKER_GEN_CONTAINER=proxy-dockergen

networks:
  default:
    external:
      name: nginx-proxy

volumes:
  conf:
  certs:
  html:
  ```
  ## Container config
  ```yaml:
      environment:
      - VIRTUAL_PORT=PORT-USED
      - VIRTUAL_HOST=WHAT.xpese.spdns.de

# in order for the proxy to see this service, it needs to be on the same network
networks:
  default:
    external:
      name: nginx-proxy
  ```