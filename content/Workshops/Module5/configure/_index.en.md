+++
menuTitle = "Configure"
title = "Configure AWS Secrets Manager"
date = 2020-07-30T11:31:12-05:00
weight = 7
pre = "<b>3. </b>"
+++

In this module you will create a new AWS Secret Manager secret for the RDS database.  We'll then use that secret in our Lambda function to securely connect to the database.

### Agenda
1. Create a new secret for the RDS database
2. Modify the RDS Lambda function to use the new Secrets Manager secret