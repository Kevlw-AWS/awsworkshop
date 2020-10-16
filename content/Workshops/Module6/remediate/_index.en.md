+++
menuTitle = "Remediate"
title = "Terminate the sleeper agent"
date = 2020-07-30T11:31:12-05:00
weight = 12
pre = "<b> </b>"
+++



**Terminate the sleeper agent**

You probably have guessed. The sleeper agent is a lambda function that subscribes to the IAM user creation event. Every time a new user is created, it automatically escalates the privilege of the user and attaches a pair of access/secret key. The key pair is then sent back to the attack. In this case, we only posted the access/secret key to our s3 bucket.

1. Go ahead to delete the lambda function that contains AgentFunction in its name. 