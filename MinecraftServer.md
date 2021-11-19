---
title: Minecraft Server
description: handle minecraf tservers
published: 1
date: 2021-11-18T17:31:18.658Z
tags: minecraft
editor: markdown
dateCreated: 2021-11-18T17:30:37.288Z
---

# Minecraft Servers
##  Update MC Mod server

1. sudo su <username>
2. Download Mod pack:
   `wget https://media.forgecdn.net/files/<first 4 digits of mod id>/<next 3 digits of mod id>/<filename from download page>`
3. unzip <filename>
4. cp <filename> serverfiles
5. chmod -R <username>:<group> serverfiles
6. chmod +x serverfiles/startserver.sh
7. ./serverfiles/startserver.sh #maybe comment out -o pipefail
8. mv start-jar minecraftserver.jar

### post-installation

cry if its not working!