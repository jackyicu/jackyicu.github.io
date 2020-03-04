---
layout: post
title:  "iptables quota control"
date:   2018-09-06 08:30:00 +0800
categories: howto
---

Use iptables and crontab to control daily,weekly, monthly quota of traffic over ports and protcols.

# Global Traffic Control 
Daily limit of all data to 1 GB

```
iptables -N QUOTA_CONTROL
iptables -F OUTPUT
iptables -P OUTPUT ACCEPT
iptables -A OUTPUT -j QUOTA_CONTROL
iptables -A QUOTA_CONTROL -m quota --quota 1000000000 -j RETURN
iptables -A QUOTA_CONTROL -j DROP

crontab -e
0 0 * * * /sbin/iptables -Z QUOTA_CONTROL
```

# Traffic control on specified ports
Daily limit of udp and tcp transfered to port 8080 to 1 GB 

```
iptables -N QUOTA_CONTROL
iptables -A OUTPUT -p tcp -m tcp --sport 8080 -g QUOTA_CONTROL
iptables -A OUTPUT -p udp -m udp --sport 8080 -g QUOTA_CONTROL
iptables -A QUOTA_CONTROL -m quota --quota 1000000000 -j ACCEPT
iptables -A QUOTA_CONTROL -j DROP

crontab -e
0 0 * * * /sbin/iptables -Z QUOTA_CONTROL
```


