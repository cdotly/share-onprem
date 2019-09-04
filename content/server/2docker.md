---
title: "Obtaining Docker Images"
date: 2019-08-09T13:23:08-05:00
draft: false
weight: 120
# menu:
#   server:
#     # parent: 'extras'
#     weight: 120
---

- Make sure that your environment supports Docker and that Docker is installed. 
- Be sure a Docker group exists on the system and that your user is part of it. If not, run `sudo groupadd docker` to create the group and `sudo usermod -a -G docker $YOURUSERNAME` (replacing $YOURUSERNAME with the username on your system)
- Run the following command and log in using the credentials supplied to you by the SpiderOak team. This is necessary in order to download the docker images. `docker login registry.spideroak.com`
- Once you have successfully logged in, pull the necessary docker images using these commands, one at a time:

```
docker pull registry.spideroak.com/share-onprem/flowblock:latest

docker pull registry.spideroak.com/share-onprem/flowcif:latest

docker pull registry.spideroak.com/share-onprem/flowkeygen:latest

docker pull registry.spideroak.com/share-onprem/flowmergecifs:latest

docker pull registry.spideroak.com/share-onprem/flowstore:latest
```
