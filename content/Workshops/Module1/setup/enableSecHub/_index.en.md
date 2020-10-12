+++
title = "Enable AWS Security Hub"
menuTitle = "Enable Security Hub"
date = 2020-07-30T14:27:09-05:00
weight = 11
chapter = true
pre = "<b></b>"
+++

Your second step is to enable AWS Security Hub.  The bucket policy findings from Amazon Macie will be sent to Security Hub.
1. Go to the [AWS Security Hub](https://console.aws.amazon.com/securityhub/home) console.
2. Click on the **Go to Security Hub** button.  
3. Do not change any selected or default options.
4. Click on the **Enable Security** Hub button.

{{% notice note %}}
Ignore the red banner indicating AWS Config not enabled in the Security Hub console.  It is not a requirement for this workshop.
{{% /notice %}}

AWS Security Hub is now enabled and will begin collecting and aggregating findings from the security services we have enabled so far.