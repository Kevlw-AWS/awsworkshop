+++
title = "Investigate why credentials are getting stolen"
menuTitle = "Investigate"
date = 2020-07-30T15:56:17-05:00
weight = 12
pre = "<b> </b>"
+++

Set up a CloudWatch alert
1. In this step, you need to create a CloudWatch alert for the privileged IAM operations, so that you can monitor and detect malicious operations. The IAM operations, AttachUserPolicy and CreateAccessKey, should not be performed by a lambda function and be closely monitored.
2. In the AWS Console, go to **CloudWatch**(click on Services->Choose CloudWatch). Then click on Rules under Events. Click the Create Rule button to create a new CloudWatch rule.
3. Choose Events by Service from the "Build event      pattern to match..." dropdown menu
4. Choose Event Pattern
5. Apply the following parameters to Event source:
    Service Name = IAM
    Event Type = AWS API call via CloudTrail
6. Choose Specific Operations Type AttachUserPolicy and  CreateAccessKey as the operations you want to monitor.
Your Event Pattern Preview should look like ![this ](/images/p1.png).
7. Click the Add target button on the right side pane
8. Choose SNS topic
9. Click the Select topic dropdown menu to select event-rule-action topic
10. Click Configure details button on the lower right corner
11. Give your Rule a name, e.g. “DetectUserChange”, then click on Create Rules
12. You will see a page listing all available rules. Click on the link to rule you just created, e.g. “DetectUserChange”.Examine the rule you just created, you should see something similar to ![this](/images/r1.png?).
13. Subscribe to the event-rule-action SNS topic with your email address. Don’t forget to confirm your email subscription.
14. Create another test user. You will receive two email notifications from the CloudWatch rule you just created