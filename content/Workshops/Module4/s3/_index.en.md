+++
title = "S3 Bucket Encryption"
date = 2020-08-18T11:04:54-05:00
weight = 8
pre = "<b>3. </b>"
+++

PCI DSS v3.2.1 *Requirement 3* dictates that protection methods like encryption are critical components in manageing the security of coldholder data.  Whether you're using the [Amazon Elastic Block Store (EBS)](https://aws.amazon.com/ebs) or the [Amazon Simple Storage Service (S3)](https://aws.amazon.com/s3/) you have the ability to encrypt data at rest.

Our Jam has deployed an S3 bucket that isn't currently encryption data at rest.  We're going to use [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) to identify the S3 bucket that we will then configure to encrypt data.  As CloudTrail logs all AWS API activity we need to make sure the S3 bucket CloudTrail is using is encrypted.

### Find the S3 bucket used by CloudTrail
1. Head to the [CloudTrail](https://us-west-2.console.aws.amazon.com/cloudtrail/home?region=us-west-2#/dashboard) dashboard
2. You should see a trail called `PCICloudTrail`
3. Click on this trail and identify where its data is being stored

![CloudTrail S3](/images/04-pci-s3-trail.png)

4. Head to the [S3 console](https://s3.console.aws.amazon.com/s3/home?region=us-west-2#) and find the bucket referenced

### Configure encryption on the S3 bucket

5. Click on the S3 bucket and then the **Properties** tab to view its configuration

{{% notice note %}}
Under **Properties**, you'll find the **Default encryption** is disabled, we'll be enabling it next
{{% /notice %}}

6. Select the **Default encryption** option.  And then select the `AWS-KMS` radio button
7. In the drop down of available keys, select the `PCIEncryptionKey` and then click **Save**

![S3 Encryption](/images/04-pci-s3-de.png)

Great, we now have encryption enabled on our S3 bucket, next lets look at how to use [AWS WAF](./waf.html) to protect public traffic.