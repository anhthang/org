---
layout: post
title: "Disable firewall in EC2 instance from AWS Console"
description: "Disable firewall in EC2 instance from AWS Console"
date: 2018-06-29
comments: false
categories: [disable firewall, ec2]
permalink: 2018/06/29-disable-firewall-in-ec2-instance-from-aws-console
---

I have locked myself out of SSH with UFW in EC2 AWS. Then, I can't reconnect.

I found this script and it works with below steps:

- Stop your problem instance
- Paste this script in `Instance Settings > View/Change User Data`

```
Content-Type: multipart/mixed; boundary="//"
MIME-Version: 1.0
--//
Content-Type: text/cloud-config; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="cloud-config.txt"
#cloud-config
cloud_final_modules:
- [scripts-user, always]
--//
Content-Type: text/x-shellscript; charset="us-ascii"
MIME-Version: 1.0
Content-Transfer-Encoding: 7bit
Content-Disposition: attachment; filename="userdata.txt"
#!/bin/bash
ufw disable
iptables -L
iptables -F
--//
```

- Start your instance and now you should be able to SSH
