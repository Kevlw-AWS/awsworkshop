+++
title = "Cleanup"
date = 2020-07-30T11:33:04-05:00
weight = 6
pre = "<b></b>"
+++

In order to prevent charges to your account we recommend cleaning up the infrastructure that was created. If you plan to keep things running so you can examine the workshop a bit more please remember to do the cleanup when you are done. It is very easy to leave things running in an AWS account, forgot about it, and then accrue charges.  

{{% notice tip %}}
If you are using this in an instructor led session, with AWS Jam you do not need to run the cleanup steps.
{{% /notice %}}
{{% notice info %}}
If you are running this in your own account. You will need to manually delete some resources before you delete the CloudFormation stacks so please do the following steps in order.
{{% /notice %}}

1. Delete the five S3 buckets created by the Module 1 CloudFormation template.  The buckets are labeled with:  
    macieworkshop-env-setup-confidentialbucket-\<random\>  
    macieworkshop-env-setup-publicbucket-\<random\>  
    macieworkshop-env-setup-internalbucket-\<random\>  
    macieworkshop-env-setup-demobucket-\<random\>  
    macieworkshop-env-setup-resultsbucket-\<random\>  

- Go to Amazon S3 console
- Click on the appropiate bucket
- Click **Delete Bucket**
- Copy and paste the name of the bucket (this is an extra verification that you actually want to delete the bucket)
- Repeat the steps above for all three buckets

2. Delete the Module 1 Cloudformation template (MacieWorkshop-Env-Setup)

- Go to the AWS CloudFormation console
- Select the appropiate stack
- Select **Action**
- Click **Delete Stack**

3. Disable Amazon Macie  
{{% notice tip %}}
Disabling Macie will remove the custom data identifier, jobs and results.
{{% /notice %}}
- Go to the Amazon Macie console
- Click on Settings on the left navigation menu
- Scroll down 
- Click **Disable Macie**

4. Disable AWS Security Hub

- Go to the AWS Security Hub console
- Click on Settings on the left navigation
- Click the General on the top navigation
- Click **Disable AWS Security Hub**
