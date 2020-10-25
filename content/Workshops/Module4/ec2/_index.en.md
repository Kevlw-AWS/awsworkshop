+++
title = "Security Groups"
date = 2020-08-18T11:04:54-05:00
weight = 10
pre = "<b>5. </b>"
+++

1. Go to the EC2 service and select Security Groups.

2. Select the `jump-sg` group and view the Inbound tab. Configure it to only allow inbound access over port `22`.

3. Select the `dbhost-sg` group and view the Inbound tab.  Configure it to only allow inbound access over port `3306`.

4. Select the `webhost-sg` and `apphost-sg` groups and view the Inbound tabs.  Configure them to only allow inbound access over ports `80/443`.
