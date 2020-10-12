+++
menuTitle = "Run the Cloudformation template"
title = "Run the cloudformation template"
date = 2020-07-30T14:27:19-05:00
weight = 12
+++

To initiate the scenario and create the infrastructure we need to deploy a cloudformation template.

{{% notice note %}}
Before you deploy the CloudFormation template feel free to view it [here](https://apj-security-workshop.s3-ap-southeast-2.amazonaws.com/macie/MacieWorkshopSetup.yml)
{{% /notice %}}

Region|Deploy
-----|-----
ap-southeast-2 (Sydney)| [![Deploy CloudFormation Template in ap-southeast-2](/images/deploy-to-aws.png)](https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=MacieWorkshop-Env-Setup&templateURL=https://apj-security-workshop.s3-ap-southeast-2.amazonaws.com/macie/MacieWorkshopSetup.yml)  


1. Click on the **Deploy to AWS** button.  This will automatically take you to the console to run the template, click **Next** to get the **Specify Details** page.
2. On the **Specify Details** section enter the necessary parameters as shown below. 

	| Parameter | Value  |
	|-----|-----|
	| Stack name | MacieWorkshop-Env-Setup  |
	| Email Address | Any valid email address you have access to  |
	
3. Once you have entered your parameters click **Next**. 
4. Click **Next** again. \(leave everything on this page at the default\).
5. Finally, scroll down and check the box to acknowledge that the template will create IAM roles and click **Create stack**.

![IAM Capabilities](/images/iam-capabilities.png)

This will bring you back to the CloudFormation console. You can refresh the page to see the stack starting to create. Before moving on, make sure the stack is in a **CREATE_COMPLETE** status as shown below.

![Stack Complete](/images/01-stack-complete.png)

{{% notice note %}}
Do not forget to check your email!
{{% /notice %}}

 You will get an email from SNS asking you to confirm the Subscription. 
 
 **Confirm the subscription** so you can receive email alerts from AWS services during the workshop. The email may take 2-3 minutes to arrive, check your spam/junk folder if it doesn’t arrive within that timeframe.