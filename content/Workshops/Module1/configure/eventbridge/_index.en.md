+++
title = "Create a EventBridge rule for remediation"
menuTitle = "EventBridge rule"
date = 2020-07-30T15:08:58-05:00
weight = 12
chapter = true
pre = "<b></b>"
+++

You have just created a custom data identifier.  Now we need to create a EventBridge rule that will automatically remediate any findings created when we use the custom data identifier to find data that is incorrectly tagged and stored.  For now we are just creating the EventBridge rule, we will shortly create the data discovery job.

Amazon EventBridge is a serverless event bus that makes it easy to connect applications together using data from your own applications, integrated Software-as-a-Service (SaaS) applications, and AWS services. See [Amazon EventBridge](https://aws.amazon.com/eventbridge/) for more information.

1. Open the [Amazon EventBridge console](https://console.aws.amazon.com/events/home)
2. Click on the **Create rule** button  

![Create rule button](/images/eventbridge-create-rule.png)

3. Enter a Name and Description

Name| Description
-----|-----
**MacieWorkshop_Remediation_Rule**|**Trigger Lambda function when Project Unicorn data is discovered**

![Name and Description](/images/eventbridge-create-rule-1.png)

4. Select **Event Pattern**
5. Select **Custom Pattern**
6. Copy and paste the event pattern below into the custom event pattern block   

````json
    {
    "source": [
        "aws.macie"
    ],
    "detail": {
        "type": [
        "SensitiveData:S3Object/CustomIdentifier"
        ]
    }
    }
````
7. Click **Save**

![Custom Event pattern](/images/eventbridge-create-rule-2.png)

8. Leave the Event bus settings as default
9. Under ***Select targets*** select ***Lambda function*** as the target to invoke when the pattern is matched.
10. Under the ***Function*** select **MacieWorkshop-Env-Setup-RemediationLambdaFunction-\<random\>**   

![Custom Event pattern](/images/eventbridge-create-rule-3.png)

11. Do not add any Tags
12. Click **Create** 