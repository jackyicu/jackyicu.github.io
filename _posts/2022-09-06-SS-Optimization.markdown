---
layout: post
title:  "Optimization for Shadowsocks Server"
date:   2018-09-06 08:30:00 +0800
categories: jekyll update
---

Optimize the shadowsocks server (Debian 9) for handling thousands of cocurrent connections.

Step 1. Edit the limits.conf.

`vi /etc/security/limits.conf`

Step 2. Add 2 lines to this file.

```
* soft nofile 51200
* hard nofile 51200

```

Step 3. Edit /etc/profile to change ulimit.

`ulimit -SHn 51200`

Step 4. Add the below lines to /etc/sysctl.d/local.conf to tune kernel.

```
# max open files
fs.file-max = 51200
# max read buffer
net.core.rmem_max = 67108864
# max write buffer
net.core.wmem_max = 67108864
# default read buffer
net.core.rmem_default = 65536
# default write buffer
net.core.wmem_default = 65536
# max processor input queue
net.core.netdev_max_backlog = 4096
# max backlog
net.core.somaxconn = 4096

# resist SYN flood attacks
net.ipv4.tcp_syncookies = 1
# reuse timewait sockets when safe
net.ipv4.tcp_tw_reuse = 1
# turn off fast timewait sockets recycling
net.ipv4.tcp_tw_recycle = 0
# short FIN timeout
net.ipv4.tcp_fin_timeout = 30
# short keepalive time
net.ipv4.tcp_keepalive_time = 1200
# outbound port range
net.ipv4.ip_local_port_range = 10000 65000
# max SYN backlog
net.ipv4.tcp_max_syn_backlog = 4096
# max timewait sockets held by system simultaneously
net.ipv4.tcp_max_tw_buckets = 5000
# turn on TCP Fast Open on both client and server side
net.ipv4.tcp_fastopen = 3
# TCP receive buffer
net.ipv4.tcp_rmem = 4096 87380 67108864
# TCP write buffer
net.ipv4.tcp_wmem = 4096 65536 67108864
# turn on path MTU discovery
net.ipv4.tcp_mtu_probing = 1

```

Step 5. `Reboot` system.

