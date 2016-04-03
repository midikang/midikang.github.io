---
layout: post
title:  "Docker network"
date:   2016-04-03 23:32:57
categories: docker
---

# Docker network

- Bridge network
- Host network
- Container network
- None network

admatoMacBook-Pro:docker_network ad$ docker run -d -P --net=none httpd
e5a11517b79fe35be6d32eea4a4c9d03bcb256d53e2493141a0b84740b6fca6b
admatoMacBook-Pro:docker_network ad$ docker ps
CONTAINER ID        IMAGE               COMMAND              CREATED                  STATUS              PORTS               NAMES
e5a11517b79f        httpd               "httpd-foreground"   Less than a second ago   Up 3 seconds                            goofy_northcutt

admatoMacBook-Pro:docker_network ad$ docker exec e5a11517b79f ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever

admatoMacBook-Pro:docker_network ad$ docker inspect e5a11517b79f |grep IPAddress
            "SecondaryIPAddresses": null,
            "IPAddress": "",
                    "IPAddress": "",
