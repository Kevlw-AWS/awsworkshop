+++
title = "Configure AWS Config Rules"
menuTitle = "Configure AWS Config Rules"
date = 2020-08-18T14:27:09-05:00
weight = 15
pre = "<b>3. </b>"
+++

#### 1. Select Config Rules

At the time this lab was being created there were [150 AWS Managed Config Rules](https://docs.aws.amazon.com/config/latest/developerguide/managed-rules-by-aws-config.html) At the time this lab was being created there were 150 AWS Managed Config Rules to choose from but the number is growing.) to choose from but the number is growing.

In this lab we will use three AWS Managed Config Rules that relate to S3. Recall that we created an S3 bucket already as part of the AWS Config setup to provide config a place to store configuration history and configuration snapshots.

The rules we will use are:
   
- [s3-bucket-server-side-encryption-enabled](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html)
- [s3-bucket-public-write-prohibited](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-write-prohibited.html)
- [s3-bucket-public-read-prohibited](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-public-read-prohibited.html)

1. Enter **s3-bucket** into the search bar and 
2. Select the three rules listed above and 

![Select Config Rules](../../../images/04-config-select-rules.png)
3. Select **Next**

#### 2. Review Config Rules
![Review Config Rules](../../../images/04-config-review-rules.png)
1. Select **Confirm**

You can now progress to the next step 