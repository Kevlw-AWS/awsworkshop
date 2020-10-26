+++
title = "IAM Password Hardening"
date = 2020-08-18T11:04:54-05:00
weight = 6
pre = "<b>1. </b>"
+++

PCI DSS sets out a number of requirements for the password management and strength of identities.  Specifically, Requirement 8 of the PCI DSS v3.2.1 standard requires the following for passwords:

- at least one uppercase character
- at least one lowercase character
- one non-alphabetic character
- one number
- minimum password length of 7
- password rotation every 90 days
- password history of 4

Let's go ahead and implement a PCI DSS compliant password policy for user ID's that are created on AWS.

1. Go to the [AWS IAM](https://console.aws.amazon.com/iam/home?region=us-west-2#/home) console
2. Click on **Account settings** on the left-hand menu
3. Click on **Set password policy**
4. Using the PCI DSS requirements as a reference, go ahead and set the AWS user policy to the same

Your password policy should look like the one below to conform to PCI DSS

![IAM Password Policy](/images/04-pci-iam-policy.png)

5. Save the new password policy

With passwords now being PCI DSS compliant lets [move on](./kms.html) to encryption key rotation using KMS.