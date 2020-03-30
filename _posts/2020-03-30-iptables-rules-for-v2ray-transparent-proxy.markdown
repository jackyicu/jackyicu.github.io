---
layout: post
title:  "iptables rules for v2ray transparent proxy"
date:   2020-03-30
categories: howto
---

Last December I bought one N1 Phicomn device from PDD, and immediately install Debian and v2ray on it to make it a side router for bypass GFW.

I found the memorry usage is extreemly high compared to v2ray running on other platform. So I tried to figure out why this happened.

Many people mentioned the UDP proxy has bugs in the issues and the maintainer @klsr marked them as a legacy problem which is not fixed yet.

So the solution might be removing the udp proxy. Here are the revised iptables rules, which originated from @toutyrater.

```
# Route Policy
ip rule add fwmark 1 table 100
ip route add local 0.0.0.0/0 dev lo table 100

# Proxy Lan
iptables -t mangle -N V2RAY
iptables -t mangle -A V2RAY -d 127.0.0.1/32 -j RETURN
iptables -t mangle -A V2RAY -d 224.0.0.0/4 -j RETURN
iptables -t mangle -A V2RAY -d 255.255.255.255/32 -j RETURN
iptables -t mangle -A V2RAY -d 192.168.0.0/16 -p tcp -j RETURN
iptables -t mangle -A V2RAY -p udp --dport 53 -j TPROXY --on-port 12345 --tproxy-mark 1
iptables -t mangle -A V2RAY -p tcp -j TPROXY --on-port 12345 --tproxy-mark 1
iptables -t mangle -A PREROUTING -j V2RAY

# Proxy Localhost Except UDP
iptables -t mangle -N V2RAY_MASK
iptables -t mangle -A V2RAY_MASK -d 224.0.0.0/4 -j RETURN
iptables -t mangle -A V2RAY_MASK -d 255.255.255.255/32 -j RETURN
iptables -t mangle -A V2RAY_MASK -d 192.168.0.0/16 -p tcp -j RETURN
iptables -t mangle -A V2RAY_MASK -j RETURN -m mark --mark 0xff
iptables -t mangle -A V2RAY_MASK -p tcp -j MARK --set-mark 1
iptables -t mangle -A OUTPUT -j V2RAY_MASK
```

I deleted the udp rules completely from localhost proxy list because it may cause errors `fialed to resolve dns on 127.0.0.1:53`. 

So here is the changes:
- Memory used before: 46%
- Memorry used after: 8%
