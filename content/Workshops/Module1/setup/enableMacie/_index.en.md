+++
title = "Enable Amazon Macie"
menuTitle = "Enable Macie"
date = 2020-07-30T14:27:03-05:00
weight = 10
chapter = true
pre = "<b></b>"
+++

Your first step is to enable Amazon Macie.  Later we will create data classification jobs to investigate the contents of your S3 buckets and Macie will also do analysis on your S3 buckets and report on any configuration changes.

1. Go to the [Amazon Macie](https://console.aws.amazon.com/macie/home) console.
2. Click on the **Get Started** button.
3. Click on the **Enable Macie** button.  If not present then Macie is already enabled.

{{% notice warning%}}
When you enable Macie for the first time, your account is automatically enrolled in the 30-day free trial for Macie. To learn more, see [Amazon Macie pricing](https://aws.amazon.com/macie/pricing/)  
If you are using Event Engine this does not apply.
{{% /notice %}}

Macie is now enabled and has begun to collect information about the S3 buckets in the account.