+++
title = "Review"
menuTitle = "Review"
date = 2020-07-30T11:04:54-05:00
weight = 10
pre = "<b>4. </b>"
+++

With our new secret successfully created using AWS Secrets Manager and our AWS Lambda function modified to use this secret instead of the hardcoded username and password, we can now validate that we're still able to query our endpoint and return records from RDS.

### Test the Updated Lambda Function

1. Head back to `Output Properties` in the Jam and copy and paste the `ApiUrl` value into your browser
2. You should get the following result if you were successful

```
Selected 3 items from RDS MySQL table
```