---
layout: post
title:  "Shadowsocks on debian 9"
date:   2018-07-25 15:10:00 +0800
categories: jekyll update
---

This tutorial is for setup of shadowsocks-libev on debian 9.

# Test IP
Once the new server is installed on your vps, test the internet connection:

`ping 0.0.0.0 # your server ip`

Destroy the server if the connection is lost.

#  Install shadowsocks-libev
## Installation
For Debian 9 (Stretch) users, please install it from stretch-backports: We strongly recommend you to install shadowsocks-libev from stretch-backports. For more info about backports please refer to Debian Backports.
```
sh -c 'printf "deb http://deb.debian.org/debian stretch-backports main" > /etc/apt/sources.list.d/stretch-backports.list' 
apt update 
apt -t stretch-backports install shadowsocks-libev
```

## Configuration

Use vi to edit configuration file and then restart shadowsocks-libev
```
vi /etc/shadowsocks-libev/config.json

{
    "server":"0.0.0.0",
    "server_port":8389, # any port
    "local_port":1081, 
    "password":"aes_password", #your password
    "timeout":60,
    "method":"aes-256-gcm",
    "local":"127.0.0.1",
    "fast_open":false
}

Restart shadowsocks-libev
```

## Test connection

Properly configurate the client and then test.
Check the server log if neccessary:

`journalctl -u shadowsocks-libev`

# Optimize connection

Activate bbr to improve internet connection.

1. create a new file

`vi /etc/sysctl.d/local.conf`


2. add these 2 lines to the file
​
```
net.core.default_qdisc = fq
net.ipv4.tcp_congestion_control = bbr
```

3. type the following commands to activate and check the status of bbr:
```
​sysctl --system
sysctl net.ipv4.tcp_available_congestion_control
sysctl net.ipv4.tcp_congestion_control
lsmod | grep bbr
```