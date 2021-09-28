+++
title = "5. Intentional Data Policies"
date = 2019-11-18T08:23:04+11:00
weight = 31
chapter = false
+++

Not all data is created equal, which means classifying data properly is crucial to its [security](https://aws.amazon.com/blogs/database/best-practices-for-securing-sensitive-data-in-aws-data-stores/). It’s important to accommodate the complex tradeoffs between a strict security posture and a flexible agile environment. A strict security posture, which requires lengthy access-control procedures, creates stronger guarantees about data security. However, such a security posture can work counter to agile and fast-paced development environments, where developers require self-service access to data stores. Design your approach to data classification to meet a broad range of access requirements. If you have no classification policy currently, public versus private is a good place to start.

To protect your data once it has been classified, we will do 2 steps in this lab: 
  1. [Use Amazon S3 to block public access](https://aws.amazon.com/blogs/aws/amazon-s3-block-public-access-another-layer-of-protection-for-your-accounts-and-buckets/) in any account that should not be able to share data through Amazon S3.
  2. [Use two different IAM roles for encryption and decryption with KMS](https://aws.amazon.com/blogs/security/new-whitepaper-available-aws-key-management-service-best-practices/). 

### Steps - Account Level Block Public Access on S3

If you have an account whereby public access should never be granted e.g. your Logging Accounts, it is a good idea to block public access at an account level. You may also choose to block public access at the individual level as well. 

1. From the AWS console, click *Services* and select *Simple Storage Service*.
2. Select *Block Public Access settings for this account*

![Select Block Public Access Settings](/images/Module-5-Image-1.png)

3. Click on *Edit* to change the Block public Access Settings for this account. 

![Click on Edit](/images/Module-5-Image-2.png)

4. Check *Block all public access* and then click *Save Changes*

![Check Block all public access](/images/Module-5-Image-3.png)

5. Type confirm into the field in order to block public access for all objects and buckets in this account. Click Confirm. 

![Type confirm](/images/Module-5-Image-4.png)

6. You should have successfully blocked all public access for this account. Future buckets and objects that are created will no longer be able to be made public. 

For more information please read the [AWS User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security.html)

### Steps - Segregate your KMS Key Admins from Key Users 

This lets you separate who should be able to create, delete, rotate and manage your customer managed keys on AWS, and those who should only be allowed to call the encrypt and decrypt functions on AWS. It is a good idea to segregate these roles and responsibilities. 

1. From the AWS console, click *Services* and select *Key Management Service*. 

2. Select Customer-managed keys from the left hand column. 

![Select customer-managed keys](/images/Module-5-Image-5.png)

3. Select one of the customer managed keys. 
4. Under Key Administrators, review who should have access to create, delete, rotate and manage your customer managed keys on AWS. 
5. Under Key Users, review who should be able to encrypt and decrypt your data on AWS. 
6. Assign the users / roles who should have the relevant permissions. 

![Assign the users/roles who should have the relevant permissions](/images/Module-5-Image-6.png)
7. Click *Switch to Policy View* to look at the results of the Key Policy you’ve applied. 
8. Note that my demo user that I provisioned Key Administrator access for is able to perform the following actions: 

![Key administrator permissions](/images/Module-5-Image-7.png)

9. Note that my basic user that I provisioned Key User access for is able to perform the following actions: 

![Key user permissions](/images/Module-5-Image-8.png)

For more information refer to [this documentation](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html)