---
layout: post
title:  "enable ipv6 on vultr vps"
date:   2020-04-02
categories: howto
---

Today I found Google Scholar banned my access from vultr ipv4 address.
So I tried to tunnel my access via v2ray with a ipv6 address.

# Quick Start

1. Check `ip_forward`, go to step 2 if you found the value is 1.

```
sysctl net.ipv4.ip_forward

net.ipv4.ip_forward = 1
```

2. Enable ipv6 for your connection

```
nano /etc/sysctl.conf
# Append the below lines to enable your ipv6 connection
net.ipv6.conf.ens3.disable_ipv6 = 0

net.ipv6.conf.all.accept_ra=2
net.ipv6.conf.eth0.accept_ra=2
```

3. Add hoss of google scholar to `/etc/hosts`

```
nano /etc/hosts

2404:6800:4008:c06::be scholar.google.com
2404:6800:4008:c06::be scholar.google.com.hk
2404:6800:4008:c06::be scholar.google.com.tw
2404:6800:4008:c06::be scholar.google.cn
```

# Proxy ipv6 traffic only on v2ray 

1. change the freedom settings

```
{
  "protocol" : "freedom",
  "sendThrough": "your vps ipv6 address"
  "domainStrategy": "UseIPv6"
}
```

2. This will not forward your dns request to a ipv4 dns server such as 8.8.8.8. 
So maybe use a ipv6 dns server or DOH server will solve this problem.
But I didn't try it anyway. Change the host file is fine enough.

# Further More

Vultr offer 2.5 USD vps sometimes, but it has ipv6-only.
Maybe cloudflare can help to proxy our ipv4 traffic to the ipv6-only vps.
It is just an idea.

# Reference:

- [How to enable IPv6 on a Vultr instance without losing network connectivity?](https://bobcares.com/blog/vultr-ipv6/)
- [V2ray Configuration Overview](https://v2ray.com/en/configuration/overview.html)
