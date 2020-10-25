+++
menuTitle = "Remediate"
title = "Terminate the sleeper agent"
date = 2020-07-30T11:31:12-05:00
weight = 12
pre = "<b>3. </b>"
+++

**Terminate the sleeper agent**

You probably have guessed. The sleeper agent is a lambda function that subscribes to the IAM user creation event. Every time a new user is created, it automatically escalates the privilege of the user and attaches a pair of access/secret key. The key pair is then sent back to the attack. In this case, we only posted the access/secret key to our s3 bucket.

Go ahead to delete the lambda function that contains `AgentFunction` in its name. 

1. Head to the [AWS Lambda](https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions) console
2. Select the option button to the left of `AgentFunction`
3. Click on **Actions** and then **Delete**

![Delete Lambda Function](/images/06-sleeperagent-lambda-delete.png)

{{% notice info %}}
Refresh the status check link provided to you by the output url link in the Jam challenge (**Output Properties**). Copy and paste the answer and submit it on the challenge site. 
{{% /notice %}}