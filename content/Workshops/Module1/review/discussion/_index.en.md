+++
title = "Jam Review"
date = 2020-07-30T11:32:55-05:00
weight = 5
pre = "<b> </b>"
+++

In this workshop you addressed data classification and fictional audit concerns using the architecture described in the diagram below.

![Macie workshop architecture](/images/macie_workshop_architecture.png)

You should now be able to do the following with Amazon Macie:
- Enable Macie
- Create Macie data classification jobs
- Create a custom data identifier
- Create a CloudWatch event triggered from a Macie finding, to fire a Lambda function 
- Understand and navigate Macie findings
- Create a suppression rule to help tune Macie findings

You were able to easily answer these questions about the data:  
- Did any of the files contain US Social Security numbers (PII)?
- Which files contained US SSN and which did not
- Which files contained references to our confidential project
- Which files contain credit card numbers?
- Which buckets are those files stored in?
- Are any of the files encrypted, are any unencrypted? 

What other questions were you able to answer with Amazon Macie?