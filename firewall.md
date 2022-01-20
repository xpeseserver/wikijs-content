---
title: Firewall
description: firewall used
published: 1
date: 2022-01-20T07:52:17.587Z
tags: server, security, docker
editor: markdown
dateCreated: 2022-01-20T07:52:17.587Z
---

# UFW
## restrict docker
Add to end of `/etc/ufw/after.rules`

```
# BEGIN UFW AND DOCKER
*filter
:ufw-user-forward - [0:0]
:ufw-docker-logging-deny - [0:0]
:DOCKER-USER - [0:0]
-A DOCKER-USER -j ufw-user-forward

-A DOCKER-USER -j RETURN -s 10.0.0.0/8
-A DOCKER-USER -j RETURN -s 172.16.0.0/12
-A DOCKER-USER -j RETURN -s 192.168.0.0/16

-A DOCKER-USER -p udp -m udp --sport 53 --dport 1024:65535 -j RETURN

-A DOCKER-USER -j ufw-docker-logging-deny -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -d 192.168.0.0/16
-A DOCKER-USER -j ufw-docker-logging-deny -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -d 10.0.0.0/8
-A DOCKER-USER -j ufw-docker-logging-deny -p tcp -m tcp --tcp-flags FIN,SYN,RST,ACK SYN -d 172.16.0.0/12
-A DOCKER-USER -j ufw-docker-logging-deny -p udp -m udp --dport 0:32767 -d 192.168.0.0/16
-A DOCKER-USER -j ufw-docker-logging-deny -p udp -m udp --dport 0:32767 -d 10.0.0.0/8
-A DOCKER-USER -j ufw-docker-logging-deny -p udp -m udp --dport 0:32767 -d 172.16.0.0/12

-A DOCKER-USER -j RETURN

-A ufw-docker-logging-deny -m limit --limit 3/min --limit-burst 10 -j LOG --log-prefix "[UFW DOCKER BLOCK] "
-A ufw-docker-logging-deny -j DROP

COMMIT
# END UFW AND DOCKER
```

## Usage

```
ufw [--dry-run] enable|disable|reload
ufw [--dry-run] default allow|deny|reject [incoming|outgoing]
ufw [--dry-run] logging on|off|LEVEL
    toggle logging. Logged packets use the LOG_KERN syslog facility. Systems configured for rsyslog
    support may also log to /var/log/ufw.log. Specifying a LEVEL turns logging on for the specified LEVEL.
    The default log level is 'low'.
ufw [--dry-run] reset
ufw [--dry-run] status [verbose|numbered]
ufw [--dry-run] show REPORT
ufw [--dry-run] [delete] [insert NUM] allow|deny|reject|limit [in|out] [log|log-all] PORT[/protocol]
ufw [--dry-run] [delete] [insert NUM] allow|deny|reject|limit [in|out on INTERFACE] [log|log-all]
    [proto protocol] [from ADDRESS [port PORT]] [to ADDRESS [port PORT]]
ufw [--dry-run] delete NUM
ufw [--dry-run] app list|info|default|update
```

### examples

`ufw status verbose`
`ufw app list`
`ufw allow 'Nginx Full'`
`ufw allow 80/tcp`
`ufw allow ssh`
`ufw [delete] allow in proto udp from 193.204.114.105 to 12.34.56.78 port 123`