+++
title = "Scenario"
date = 2020-07-30T11:43:23-05:00
weight = 12
pre = "<b></b>"
+++


1. Think about all the ways an attacker can get back to the account - IAM users, overly-permissive assumable role, faulty lambda functions, compromised EC2 instances, misconfigured WAF, instance profiles.
2. Long-term persistent credentials (access/secret key, login id/password) are the easiest way for an attacker to get into the door.
3. Use CloudWatch to detect privileged IAM operations, especially operations that creates long-term credentials automatically by a lambda function.
**VERY IMPORTANT!! The CloudWatch rule should only monitor the "specific" privileged IAM operations**

