+++
title = "Investigate why credentials are getting stolen"
menuTitle = "Investigate"
date = 2020-07-30T15:56:17-05:00
weight = 12
pre = "<b>2. </b>"
+++

### Create a new user

The description of the challenge mentioned the attacker only came back after a new user was created.  So go ahead and create a new user with AWS Management Console access.  Do not attach any permission to the user, or add the user to any group.  (You will receive an error message if you attach any permission to the user.  It’s ok to ignore the message as the user will be created without permission.)  Observe what happens next.  You may have to refresh the Permission page manually.

1. Go to the [AWS IAM Console](https://console.aws.amazon.com/iam/home?region=us-east-1#)
2. Click on the **User** menu and **Add user** button
3. Give your user a username and select both checkboxes for the type of access
4. Click **Next** on the rest of the pages

![Create User](/images/06-sleeperagent-create-user.png)

5. Go back to your new user and look at the roles assigned to your user, what do you see?

{{% notice note %}}
Did you see a ReadOnlyAccess policy automatically attached to the user you just created?  In this challenge, we only attached ReadOnlyAccess to this user but it’s just as easy to attach an Admin policy or any other policy to the newly created user.
{{% /notice %}}

![Create User](/images/06-sleeperagent-view-user.png)

An attacker can also enumerate all existing users and attach privileged policies to any existing user or role if they have sufficient permission to do so.

Go to your [S3 bucket](https://s3.console.aws.amazon.com/s3/home?region=us-east-1).  Under `“jam-agent-xxxxxxxxxxxxxxxxxx”` bucket, examine the content of the key.txt file.  It contains the access key and secret key of the user you just created.  The attacker could have easily posted the credential to a Command-and-Control center web site.  Imagine what he can do with full admin rights to your account.

### Set up a CloudWatch Alert

In this step, you need to create a CloudWatch alert for the privileged IAM operations, so that you can monitor and detect malicious operations.  The IAM operations, `AttachUserPolicy` and `CreateAccessKey`, should not be performed by a lambda function and be closely monitored. 

In the AWS Console, go to [CloudWatch](https://console.aws.amazon.com/cloudwatch/home?region=us-east-1#).  Then click on Rules under Events.  

1. Click the Create Rule button to create a new CloudWatch rule
2. Choose Event Pattern
3. Choose Events by Service from the "Build event pattern to match..." dropdown menu

Serice Name | Event Type
----- | -----
IAM | AWS API call via CloudTrail

4. Choose Specific Operations
5. Type `AttachUserPolicy` and `CreateAccessKey` as the operations you want to monitor

![CloudWatch Rule](/images/06-sleeperagent-cw-rule.png)

6. Click the Add target button on the right side pane
7. Choose SNS topic
8. Click the Select topic dropdown menu to select `event-rule-action` topic
9. Click **Configure details** button on the lower right corner
10. Give your Rule a name, e.g. `DetectUserChange`, then click on **Create Rules**
11. You will see a page listing all available rules. Click on the link to rule you just created, e.g. `DetectUserChange`.  Examine the rule you just created,  you should see something similar to this

![CloudWatch Rule Finished](/images/06-sleeperagent-cw-rule-finished.png)

### Bonus Step | Subscribe to alerts

1. Subscribe to the event-rule-action SNS topic with your email address

{{% notice tip %}}
Don’t forget to confirm your email subscription
{{% /notice %}}

2. Create another test user

{{% notice info %}}
You should receive two email notifications from the CloudWatch rule you just created
{{% /notice %}}