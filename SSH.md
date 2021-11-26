---
title: SSH
description: how the sshd_config should look like
published: 1
date: 2021-11-26T11:31:13.355Z
tags: ssh
editor: markdown
dateCreated: 2021-11-26T11:31:13.355Z
---

# SSH
## Config location
`nano /etc/ssh/sshd_config`

## Config data
`#	$OpenBSD: sshd_config,v 1.104 2021/07/02 05:11:21 dtucker Exp $`
 
`# This is the sshd server system-wide configuration file.  See`
`# sshd_config(5) for more information.`

`# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin`

`# The strategy used for options in the default sshd_config shipped with`
`# OpenSSH is to specify options with their default value where`
`# possible, but leave them commented.  Uncommented options override the`
`# default value.`

`Include /etc/ssh/sshd_config.d/*.conf`

`Port 22`

`# Authentication:`

`PermitRootLogin no`
`MaxAuthTries 1`
`MaxSessions 1`

`PubkeyAuthentication yes`

`# To disable tunneled clear text passwords, change to no here!`
`PasswordAuthentication no`
`PermitEmptyPasswords no`

`# Change to yes to enable challenge-response passwords (beware issues with`
`# some PAM modules and threads)`
`KbdInteractiveAuthentication no`

`UsePAM yes`

`X11Forwarding no`

`# Allow client to pass locale environment variables`
`AcceptEnv LANG LC_*`

`# override default of no subsystems`
`Subsystem	sftp	/usr/lib/openssh/sftp-server`

`# allow local ssh michi with password`
`Match Address 10.0.0.1`
`AllowUsers michael`
`PermitRootLogin yes`
`PasswordAuthentication yes`
