+++
title = "Attack Simulation"
menuTitle = "Attack Simulation"
date = 2020-07-30T11:30:52-05:00
weight = 7
pre = "<b>2. </b>"
+++

Now that you have detective and responsive controls setup, you'll be running another CloudFormation template which will simulate the actual attack you will be investigating.

## Deploy the CloudFormation template

To initiate the attack simulation you will need to run the module 2 CloudFormation template: 

{{% notice note %}}
Before you deploy the CloudFormation template feel free to view it [here](https://apj-security-workshop.s3-ap-southeast-2.amazonaws.com/cfn/02-aws-jam-threat-detection-response-attack-simulation-nom.yml)
{{% /notice %}}

Region|Deploy
-----|-----
ap-southeast-2 (Sydney)| <a href="https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=ThreatDetectionWksp-Attacks&templateURL=https://apj-security-workshop.s3-ap-southeast-2.amazonaws.com/cfn/02-aws-jam-threat-detection-response-attack-simulation-nom.yml" target="_blank">![Deploy CloudFormation Template in ap-southeast-2](/images/deploy-to-aws.png)</a>

1. Click the **Deploy to AWS** button above.  This will automatically take you to the console to run the template. 

2. The name of the stack will be automatically populated but you are free to change it, after which click **Next**, then **Next** again (leave everything on this page at the default).  

3. Finally, acknowledge that the template will create IAM roles and click **Create**

![IAM Capabilities](/images/iam-capabilities.png)

This will bring you back to the CloudFormation console. You can refresh the page to see the stack starting to create. Before moving on, make sure the stack is in a **CREATE_COMPLETE** status as shown below.

![Stack Complete](/images/02-stack-complete.png)

{{% notice info %}}
If this fails with the error message ***\[IAM_CAPABILITY\]***, please acknowledge that the template will create IAM roles, from the previous step
{{% /notice %}}

## Architecture overview

Below is a diagram of the setup after the module 2 CloudFormation stack is created.

![Module 2 Diagram](/images/02-diagram-module2-3v2.png)

{{% notice info%}}
Please note it will take at least **20 minutes** after the 2nd CloudFormation template has completed before you will start seeing findings.
{{% /notice %}}