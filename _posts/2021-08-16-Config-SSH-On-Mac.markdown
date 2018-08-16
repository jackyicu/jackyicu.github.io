---
layout: post
title:  "Config ssh on macOS"
date:   2018-08-15 10:10:00 +0800
categories: jekyll update
---

It is more productive to use a configuration file to manage multiple remote login via ssh on macOS.

Step 1. creat a configuration file for ssh.

`vi ~/.ssh/config`

Step 2. add configurations to this blank file.

```
Host dev
    Hostname    www.example.com
    Port    22
    User    username
    IdentityFile    ~/.ssh/your_key
```

Step 3. save the file and login remote server via shortname.

`ssh dev`



