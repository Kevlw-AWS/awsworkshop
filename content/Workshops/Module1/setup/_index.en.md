+++
title = "Setup and Environment configuration"
menuTitle = "Setup"
date = 2020-07-30T11:30:52-05:00
weight = 6
pre = "<b>1. </b>"
+++

In this first module you will configure your environment.  You will enable Amazon Macie and AWS Security Hub and then run a CloudFormation template to create all the S3 buckets and populate them with data to scan.  The final step will be to finish the configuaration of Amazon Macie by completing the setup of an S3 bucket for storage of discovery results.  

### Agenda
1. Enable Amazon Macie
2. Enable Amazon Security Hub
3. Run the initial cloudformation template
4. Configure Macie to export findings to an S3 Bucket