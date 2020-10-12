+++
title = "Review Security Hub Alerts"
date = 2020-07-30T15:56:00-05:00
weight = 11
chapter = true
pre = "<b></b>"
+++

You will now pivot to Security Hub and review the alerts forwarded by Macie.  

Macie generates policy findings when the policies or settings for an S3 bucket are changed in a way that reduces the security of the bucket and its objects.  These policy findings are forwarded to Security Hub.  In AWS Security Hub you can review the findings, create a custom Insight, or take action using automation workflows.

The full list of policy findings can be found in [the documentation](https://docs.aws.amazon.com/macie/latest/user/findings-types.html)

1. Open the [Security Hub console](https://console.aws.amazon.com/securityhub/home#/summary)
2. Verify that you have Amazon Macie alerts flowing into Security Hub.  Look at the panel labeled **Latest findings from AWS integrations**.
3. Click on the link **See Findings** to filter on Amazon Macie findings.  
![Security Hub Findings from AWS integrations](/images/sec-hub-latest-findings.png)  
4. You should see a list of findings and the filters should resemble the one in the image below.  
![Filter to see Amazon Macie findings](/images/sec-hub-insight-1.png)   
5. Click on **Block Public Access settings are disabled for the S3 bucket** link under the ***Title*** column.
> This expands the alert and opens the details panel.  
6. Click on **Resources** in the information panel to expand the details and see which resources are affected.

{{% notice note%}}
The information panel not only gives you which resources are affected and the severity but also explains why the finding was created.
{{% /notice %}}

![Detail panel for Amazon Macie findings](/images/sec-hub-insight-2.png)   
7. Click on the second alert, **Encryption is disabled for the S3 bucket** to view the details and reasons for the finding.
