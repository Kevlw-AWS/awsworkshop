+++
title = "Configure Conformance Pack"
menuTitle = "Configure Conformance Pack"
date = 2020-08-18T14:27:09-05:00
weight = 20
pre = "<b>3. </b>"
+++

#### 1. Source Your AWS account ID
You will need to note your AWS account ID.
 
You can find by clicking on the dropdown beside your account name on the top menubar.
![AWS Account ID](../../../images/04-conformance-pack-accountID.png)

#### 2. Update the Operational Best Practices for S3 sample template

1. In a Text Editor
2. Open the **s3-best-practices-with-remediation-pack.yaml** 
3. Replace **ACCOUNT_ID_PLACEHOLDER** on with your AWS Account Id on lines : 
- 34
- 71
- 130
- 170 
![Conformance pack code](../../../images/04-conformance-pack-code.png)
4. Enter the Account ID as a **number only - with no dashes**.
5. Save your changes

You can now progress to the next step 