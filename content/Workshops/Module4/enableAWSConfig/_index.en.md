+++
title = "Enable AWS Config"
menuTitle = "Enable AWS Config"
date = 2020-08-18T14:27:09-05:00
weight = 10
pre = "<b>2. </b>"
+++

First we need to enable AWS Config and begin tracking of your resources.

#### 1. Access the AWS Config Console
1. Go to the [AWS Config](https://console.aws.amazon.com/config/home) console.
2. Follow one of the below:

**If this is your first time using AWS Config**

Select **Get Started** from the AWS Config intro screen.
![Getting Started](../../../images/04-config-getting-started.png)

**If you've already used AWS Config**

You will start at the AWS Config Dashboard, select **Settings** on the menu to the left.

#### 2. Select Resources to track

1. On the Settings page, under **Resource types to record**, select 
- **Record all resources supported in this region** checkbox and 
- **Include global resources** checkbox
![Resource tracking](../../../images/04-config-resource-tracking.png)

Checking these two boxes means that AWS Config will record configuration changes for all supported resources all resources as well as configuration changes for AWS Identity and Access Management (IAM) resources which are global resources. Global resources are not tied to an individual region and can be used in all regions.

#### 3. Create a Bucket for configuration history
AWS Config needs a place to store configuration history and configuration snapshot files, we will use [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) to provide this storage space - what AWS calls an S3 Bucket.

Under Amazon S3 bucket, select **Create a bucket** to have the Amazon S3 bucket created automatically.

This S3 bucket will be used to store the history used by Config, but to keep things simple and remove the need to create a second Bucket, we will be applying the Config Rules to this same S3 Bucket.


#### 4. Optional - Set-up notifications
You can leave the settings under **Amazon SNS** topic as is, or as an extra activity later
 
1. Check the box for **Stream configuration changes and notifications to an Amazon SNS topic**, and then 
2. Select **Create a topic**, and 
3. Give the SNS Topic a name, something like ***AWS-Config-Alerts***, or whatever you like.
![Resource tracking](../../../images/04-config-sns-notifications.png)

    
This will enable AWS Config to send us configuration changes and notifications via Amazon Simple Notification Service (SNS).

#### 5. Check AWS Config access
There is no need to change any settings in this section, Create AWS Config service-linked role should already be selected.

{{% notice note %}}
It is worth taking a moment to understand that for AWS Config to access other services like S3 and SNS we need to grant it permissions. This step crates a role for Config that will allow Config to access the S3 bucket and the SNS topic we set-up in the steps above.{{% /notice %}}

1. Click **Next**
2. Click **Next** again.
3. Click **Skip** to go to the Review page and Click **Confirm**

You can now progress to the next step 