+++
title = "Encryption Key Rotation"
date = 2020-08-18T11:04:54-05:00
weight = 7
pre = "<b>2. </b>"
+++

PCI DSS v3.2.1 specifies that organisations maintain strong management of their cryptographic keys.  Under *Requirement 3.6.4* it is required that keys be rotated after at the end of thier cryptoperiod.  AWS provides customers with the [AWS Key Management Service (KMS)](https://aws.amazon.com/kms/) which makes the management of keys easy, including rotating keys when needed.

This lab has automatically deployed a KMS key for you.  Let's go and enable key rotation for that KMS key.

1. Head to the [KMS](https://us-west-2.console.aws.amazon.com/kms/home?region=us-west-2#/kms/keys) console
2. Find a key called `PCIEncryptionKey` and click on the key

{{% notice note %}}
If you'd like to read through KMS' capabilities the [KMS FAQ](https://aws.amazon.com/kms/faqs/) is a good place to start
{{% /notice %}}

3. Look through the properties on the KMS key
4. Head to the **Key rotation** tab
5. Check the box `Automatically rotate this CMK every year`

![KMS Key Rotation](/images/04-pci-kms-rotate.png)

6. Click **Save** to commit your changes

With KMS key rotation checked off our list, lets tackle [S3 Bucket Encryption](./s3.html) next.