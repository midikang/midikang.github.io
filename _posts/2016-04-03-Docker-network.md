---
layout: post
title:  "Docker network"
date:   2016-04-03 23:32:57
categories: docker
---

# Docker network

- Bridge network

  $ docker run -d -P --net=bridge httpd
  fa605c362acb87070ff0a54a730bff7e0b07ecd8f4afc822232d48c8379b365f
  
  admatoMacBook-Pro:docker_network ad$ docker ps
  CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                   NAMES
  fa605c362acb        httpd               "httpd-foreground"   55 seconds ago      Up 54 seconds       0.0.0.0:32768->80/tcp   reverent_snyder
  
  admatoMacBook-Pro:docker_network ad$ docker exec fa605c362acb ip a
  1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
      link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
      inet 127.0.0.1/8 scope host lo
         valid_lft forever preferred_lft forever
      inet6 ::1/128 scope host
         valid_lft forever preferred_lft forever
  14: eth0@if15: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
      link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
      inet 172.17.0.2/16 scope global eth0
         valid_lft forever preferred_lft forever
      inet6 fe80::42:acff:fe11:2/64 scope link
         valid_lft forever preferred_lft forever


- Host network
- Container network
- None network
