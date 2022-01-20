---
title: Reverse Proxy
description: SSL and subdomain ur containers
published: 1
date: 2022-01-20T07:46:51.778Z
tags: https, nginx, proxy, ssl, web
editor: markdown
dateCreated: 2022-01-15T12:26:20.341Z
---

# Caddy-Reverse-Proxy

This is a webserver written in GO. It automatically redirects HTTP to HTTPs and generates SSL-Certificates via Lets Encrypt.
Also we use duckdns.org so we can create sub-sub-domains for our services.  

## install
```
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo tee /etc/apt/trusted.gpg.d/caddy-stable.asc
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

## apply changes
`sudo systemctl restart caddy`

## Config file
/etc/caddy/Caddyfile
```
{
    http_port 80
    https_port 443

    email xpeseserver@gmail.com

}
xpese.spdns.de {
    redir https://xpese.duckdns.org{uri}
}
xpese.duckdns.org {
    reverse_proxy localhost:3002
    log {
        output file /var/log/caddy/index.access.log {
                roll_size 3MiB
                roll_keep 5
                roll_keep_for 48h
        }
        format console
    }
    encode gzip zstd
}

dash.xpese.duckdns.org {
    root * /var/www/dash
    file_server /static/*
    log {
        output file /var/log/caddy/dash.access.log {
                roll_size 3MiB
                roll_keep 5
                roll_keep_for 48h
        }
        format console
    }
    encode gzip zstd
    php_fastcgi unix//run/php/php7.4-fpm.sock

}
wiki.xpese.duckdns.org {
    reverse_proxy localhost:3000
    log {
        output file /var/log/caddy/wiki.access.log {
                roll_size 3MiB
                roll_keep 5
                roll_keep_for 48h
        }
        format console
    }
    encode gzip zstd
}
up.xpese.duckdns.org {
    reverse_proxy localhost:3001
    log {
        output file /var/log/caddy/up.access.log {
                roll_size 3MiB
                roll_keep 5
                roll_keep_for 48h
        }
        format console
    }
    encode gzip zstd
}
file.xpese.duckdns.org {
    reverse_proxy localhost:8080
    log {
        output file /var/log/caddy/file.access.log {
                roll_size 3MiB
                roll_keep 5
                roll_keep_for 48h
        }
        format console
    }
    encode gzip zstd
}
sinus.xpese.duckdns.org {
    reverse_proxy localhost:8087
    log {
        output file /var/log/caddy/sinus.access.log {
                roll_size 3MiB
                roll_keep 5
                roll_keep_for 48h
        }
        format console
    }
    encode gzip zstd
}
```