+++
title = "S3 Bucket Encryption"
date = 2020-08-18T11:04:54-05:00
weight = 8
pre = "<b>3. </b>"
+++

1. Within `CloudTrail`, view the available trails to find the `PCICloudTrail`.

2. For the `PCICloudTrail`, review the storage location to identify the S3 bucket.

3. Go to the S3 menu to select the trail bucket and view its properties.

4. Under properties, select the default encryption option.  And then select the `AWS-KMS` radio button.

5. In the drop down of available keys, select the `PCIEncryptionKey` and then save.
