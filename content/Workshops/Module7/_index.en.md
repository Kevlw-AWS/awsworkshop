+++
title = "7. Validate IAM roles"
date = 2019-11-18T08:23:04+11:00
weight = 30
chapter = false
+++

As you operate your AWS accounts to iterate and build capability, you may end up creating multiple IAM roles that you discover later you don’t need. Use [AWS IAM Access Analyzer](https://aws.amazon.com/iam/features/analyze-access/) to review access to your internal AWS resources and determine where you have shared access outside your AWS accounts. If you have already created multiple roles, [you can search for unused IAM roles](https://aws.amazon.com/blogs/security/continuously-monitor-unused-iam-roles-aws-config/) and remove them.

### Use IAM Access Analyzer to review access to internal AWS resources from outside your zone of trust

1. From the AWS console, click *Services* and select *AWS Identity and Access Manager**. *
2. On the left hand side, select *Access Analyzer*.

![Select Access Analyzer](/images/Module-7-Image-1.png)

3. Select *Create Analyzer*. The cost of turning on Access Analyzer is free. 

![Select Create Analyzer](/images/Module-7-Image-2.png)

4. Enter an Analyzer name, and select your zone of Trust. If using AWS Organizations, you may choose to turn on Access Analyzer for your organization, and not just your current account. 

![Enter Analyzer name](/images/Module-7-Image-3.png)

5. Click *Create Analyzer*. The Analyzer will immediately start looking for external access granted to IAM roles, KMS keys and S3 buckets. Findings can be accessed through the Access Analyzer dashboard. 

For more information refer to our [documentation.](https://docs.aws.amazon.com/IAM/latest/UserGuide/what-is-access-analyzer.html)