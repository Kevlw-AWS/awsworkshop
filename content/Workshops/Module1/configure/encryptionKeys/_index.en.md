+++
title = "Macie and KMS Encryption Keys"
menuTitle = "Macie and KMS Keys"
date = 2020-07-30T15:08:24-05:00
weight = 10
chapter = true
pre = "<b> </b>"
+++

In order for Amazon Macie to correctly scan an object in your S3 bucket that is encrypted with a customer managed KMS key, the Macie service role needs to be given permssion to use the key.  The Confidential bucket in the workshop is encrypted with a KMS key and the correct permissions have been assigned to the key to provide you with an example.  

You can read the documentation for Macie [supported encryption types](https://docs.aws.amazon.com/macie/latest/user/discovery-supported-encryption-types.html) for more information.  

View the permissions for the KMS keys in this workshop in the [KMS Console](https://console.aws.amazon.com/kms/home#/kms/keys).  Look for the key alias ***MacieWorkshop-Env-Setup-confidential-bucket-encryption-key***.  

The JSON policy that has been applied to the CMK-KMS key is shown below for your information.  ***\<Account Number\>*** will be the account number of the account you are using.

```json
        {
            "Sid": "Allow Macie Service Role to use the key",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::<ACCOUNT NUMBER>:role/aws-service-role/macie.amazonaws.com/AWSServiceRoleForAmazonMacie"
            },
            "Action": [
                "kms:DescribeKey",
                "kms:Encrypt",
                "kms:Decrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey"
            ],
            "Resource": "*"
        }
```