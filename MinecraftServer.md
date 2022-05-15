---
title: Minecraft Server
description: handle minecraf tservers
published: 1
date: 2022-05-15T19:24:39.090Z
tags: minecraft
editor: markdown
dateCreated: 2021-11-18T17:30:37.288Z
---

# Minecraft Servers
##  Update MC Mod server

1. sudo su `<username>`
2. Download Mod pack:
   `wget https://media.forgecdn.net/files/<first 4 digits of mod id>/<next 3 digits of mod id>/<filename from download page>`
3. unzip `<filename>`
4. cp `<filename>` serverfiles
5. chmod -R `<username>`:`<group>` serverfiles
6. chmod +x tartserver.sh
7. cd ./serverfiles/
8. ./startserver.sh #quit when running
9. mv `serverstarter-x.x.x.jar` minecraft_server,jar

### post-installation

cry if its not working!