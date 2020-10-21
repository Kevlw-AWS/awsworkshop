+++
title = "Setup configuration"
menuTitle = "Setup"
date = 2020-07-30T11:30:52-05:00
weight = 6
pre = "<b>1. </b>"
+++

In this first module you will be configuring your environment to be ready for encrypting the spoilers.  You will be running one CloudFormation template which will automate the creation of S3 bucket, the unencrypted spoiler S3 bucket and creating the KMS key that Clinton has created (which he has not granted you access to).

**Agenda**
 
1. Run the initial CloudFormation Template – 5 min
2. Verify the account inventory - 2 min



## Deploy the AWS CloudFormation template

To initiate the scenario and configure your environment you will need to run the  CloudFormation template: 

{{% notice note %}}
Before you deploy the CloudFormation template feel free to view it [here](https://github.com/awsrossw/aws-scaling-threat-detection-workshop/tree/EventEngine/templates/TOBEUPLOADED)
{{% /notice %}}

Region| Deploy
------|-----
AP SOUTHEAST 2 (Sydney) | <a href="https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=SpoilerAlert&templateURL=https://s3-us-west-2.amazonaws.com/sa-security-specialist-workshops-us-west-2/threat-detect-workshop/staging/03-environment-setup-nom.yml" target="_blank">![Deploy in ap-southeast-2](/images/deploy-to-aws.png)</a>

1. Click the **Deploy to AWS** button above.  This will automatically take you to the console to run the template, click Next to get to the Specify Details page. 

2. Click **Next**. \(leave everything on this page at the default\)

3. Finally, scroll down and check the box to acknowledge that the template will create IAM roles and click **Create**.

![IAM Capabilities](/images/iam-capabilities.png)

This will bring you back to the CloudFormation console. You can refresh the page to see the stack starting to create. Before moving on, make sure the stack is in a **CREATE_COMPLETE** status 

![Stack Created](/images/03-cfn-stack-success.png)
4. Now click on the completed stack "SpoilerAlert" and click on "Outputs". Note down ARN of the KMS key and the name of the unencrypted spoiler S3 bucket. 

![Stack Created](/images/03-cfn-output.png)

After you have successfully setup your environment and verified the output, you can proceed to the next module.