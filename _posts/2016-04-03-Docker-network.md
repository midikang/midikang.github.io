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

  admatoMacBook-Pro:docker_network ad$ ifconfig | grep -A 2 en1:
  
  en1: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
  	ether 68:a8:6d:43:95:56
  	inet6 fe80::6aa8:6dff:fe43:9556%en1 prefixlen 64 scopeid 0x5
  	inet 192.168.31.134 netmask 0xffffff00 broadcast 192.168.31.255
  	nd6 options=1<PERFORMNUD>
  	media: autoselect
  	status: active

  admatoMacBook-Pro:docker_network ad$ docker run -d --net=host httpd
  efef0f554f31ce3516ca520a8262a531076a4cb08bd61f013adcddd5321e4f77

  admatoMacBook-Pro:docker_network ad$ docker ps
  CONTAINER ID        IMAGE               COMMAND              CREATED             STATUS              PORTS                   NAMES
  efef0f554f31        httpd               "httpd-foreground"   32 seconds ago      Up 31 seconds                               tender_shockley
  fa605c362acb        httpd               "httpd-foreground"   12 minutes ago      Up 12 minutes       0.0.0.0:32768->80/tcp   reverent_snyder
  
  admatoMacBook-Pro:docker_network ad$ docker exec efef0f554f31 ip a
  
  1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
      link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
      inet 127.0.0.1/8 scope host lo
         valid_lft forever preferred_lft forever
      inet6 ::1/128 scope host
         valid_lft forever preferred_lft forever
  2: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN group default
      link/ether 5a:f0:23:bc:f0:37 brd ff:ff:ff:ff:ff:ff
  3: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
      link/ether 08:00:27:8a:b8:b2 brd ff:ff:ff:ff:ff:ff
      inet 10.0.2.15/24 brd 10.0.2.255 scope global eth0
         valid_lft forever preferred_lft forever
      inet6 fe80::a00:27ff:fe8a:b8b2/64 scope link
         valid_lft forever preferred_lft forever
  4: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
      link/ether 08:00:27:94:a2:02 brd ff:ff:ff:ff:ff:ff
      inet 192.168.99.100/24 brd 192.168.99.255 scope global eth1
         valid_lft forever preferred_lft forever
      inet6 fe80::a00:27ff:fe94:a202/64 scope link
         valid_lft forever preferred_lft forever
  5: br-7eff80c2a44b: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
      link/ether 02:42:dd:76:f2:ed brd ff:ff:ff:ff:ff:ff
      inet 172.18.0.1/16 scope global br-7eff80c2a44b
         valid_lft forever preferred_lft forever
  6: br-8b19f90ca18e: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
      link/ether 02:42:ec:bb:22:9a brd ff:ff:ff:ff:ff:ff
      inet 172.19.0.1/16 scope global br-8b19f90ca18e
         valid_lft forever preferred_lft forever
  7: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
      link/ether 02:42:71:7e:b9:58 brd ff:ff:ff:ff:ff:ff
      inet 172.17.0.1/16 scope global docker0
         valid_lft forever preferred_lft forever
      inet6 fe80::42:71ff:fe7e:b958/64 scope link
         valid_lft forever preferred_lft forever
  15: vethf7bbb36@if14: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default
      link/ether 1a:d1:2b:d2:5d:4b brd ff:ff:ff:ff:ff:ff
      inet6 fe80::18d1:2bff:fed2:5d4b/64 scope link
         valid_lft forever preferred_lft forever
  
- Container network

admatoMacBook-Pro:docker_network ad$ docker images
REPOSITORY                     TAG                 IMAGE ID            CREATED             SIZE
composetest_python-web         latest              4273b715025a        8 days ago          683.8 MB
admatoMacBook-Pro:docker_network ad$ docker run -d -P --net=bridge 4273b715025a
75c23712f6c0fb39e217650dac088a3ff1ebaed2eab2f40769b83b21d5812640
admatoMacBook-Pro:docker_network ad$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
75c23712f6c0        4273b715025a        "/bin/sh -c 'python a"   9 seconds ago       Up 9 seconds                            backstabbing_wing
admatoMacBook-Pro:docker_network ad$ docker exec 75c23712f6c0 ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
20: eth0@if21: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.2/16 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:acff:fe11:2/64 scope link
       valid_lft forever preferred_lft forever
admatoMacBook-Pro:docker_network ad$ docker run -it --net=container:backstabbing_wing ubuntu
root@75c23712f6c0:/# ifconfig
eth0      Link encap:Ethernet  HWaddr 02:42:ac:11:00:02
          inet addr:172.17.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
          inet6 addr: fe80::42:acff:fe11:2/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:8 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:648 (648.0 B)  TX bytes:648 (648.0 B)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

- None network
