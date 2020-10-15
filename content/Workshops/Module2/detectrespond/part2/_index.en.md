+++
title = "Compromised EC2 instance"
menuTitle = "Compromised EC2 instance"
date = 2020-07-30T11:30:52-05:00
weight = 9
+++

### Detect and investigate 

Now that you've addressed the compromised IAM credential you need focus in on how the attacker was able to compromise the EC2 instance. It's this compromise which allowed them to query the instance metadata and steal the credentials.

**Explore findings related to the instance ID (AWS Security Hub)**

When investigating the compromised IAM credential you discovered that it was from an IAM role for EC2 and identified the EC2 instance ID from the principal ID of the finding. Using the instance ID __(that you previously copied, it starts with an ‘i’, such as i-08fa26ffb15a66f5a)__ you can use AWS Security Hub to start investigating the findings.  To start, you are going to research the GuardDuty findings related to the EC2 instance.

1. Go to the <a href="https://us-west-2.console.aws.amazon.com/securityhub/home?region=us-west-2#/findings" target="_blank">AWS Security Hub</a> console.
2. The link should take you to the **Findings** section (if not, click on **Findings** in the navigation on the left).
	* Add a filter by clicking in the **Add filter** box and scrolling down to **Product Name**, and paste in the word `GuardDuty`.

	* Use your browser's find function **Control-F** and paste in the `<Instance ID>` you copied earlier (from the principal ID you gathered in the GuardDuty finding). 

    * Now copy the <a href="https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html" target="_blank">Amazon Resource Name (ARN)</a> from the **Resource ID** for the first match. The ARN will look something like this `arn:aws:ec2:us-west-2:166199753942:instance/i-0efc5172a5d7ecc6b`

    * Add one more filter by clicking the **Add filter** box again and selecting **Resource ID** and paste in the ARN from the previous step
	
	!!! question "What GuardDuty findings do you see related to this instance ID?"
	
<!--3. Click in the **Add filter** box:
	* Scroll down to **Resource ID**, change the operator to **CONTAINS** and paste in the `<Instance ID>` you copied earlier (from the principal ID you gathered in the GuardDuty finding). 
	* Add another filter by again clicking in the **Add filter** box and scrolling down to **Product Name**, and paste in the word `GuardDuty`.
-->

One of the findings should indicate that the EC2 instance is communicating with an IP address on a threat list (**disallowed IP**) which adds further evidence to the conclusion that the instance has been compromised. The other finding should indicate that a system at a particular IP address is performing an SSH brute force attack against your instance.  You now need to investigate if the SSH brute force attack was successful and if that is what allowed the attacker to gain access to the instance.

**Determine if ssh password authentication is enabled on the EC2 instance (AWS Security Hub)**

Automated responses to threats can do many things. For example, you could have an trigger that helps gather information about the threat that could then be used in the investigation by the security team. With that option in mind, we have a CloudWatch event rule in place that will trigger an <a href="https://aws.amazon.com/inspector/" target="_blank">Amazon Inspector</a> scan of an EC2 instance when GuardDuty detects a particular attack. We will use AWS Security Hub to view the findings from Inspector. We want to determine if the SSH configuration adheres to best practices. 

1. Go to the <a href="https://us-west-2.console.aws.amazon.com/securityhub/home?region=us-west-2#/findings" target="_blank">AWS Security Hub</a> console.
2. The link should take you to the **Findings** section (if not, click on **Findings** in the navigation on the left). 
    * Add a filter by clicking in the **Add filter** box and scrolling down to **Product Name**, and paste in the word `Inspector`.
	* Use your browser's find function **Control-F** and paste in `password authentication over SSH`
    * The finding may not be on the first page of findings, use the `>` to move to the next page.

<!-- Click in the **Add filter** box:
* Scroll down to **Title**, change the operator to **CONTAINS** and paste in `password authentication over SSH`.
-->

Click on the finding regarding SSH and password authentication for the instance that experienced the SSH brute force attack and review.

<!--
1. Go to [AWS Security Hub](https://us-west-2.console.aws.amazon.com/securityhub/) in the AWS Management Console.
2. On the left navigation, click on **Explore Findings**
3. Add the following filter:
	* **Keyword: `password authentication over SSH`** 
	* **Provider: Inspector**
4. In the results do you see a finding regarding SSH and password authentication for the instance that experienced the SSH brute force attack? 
-->

!!! info "If you do not see any findings after a while, there may have been an issue with your Inspector agent.  Go to the <a href="https://us-west-2.console.aws.amazon.com/inspector" target="_blank">Inspector</a> console, click on **Assessment Templates**, check the template that starts with **threat-detection-wksp**, and click **Run**.  Please allow **15 minutes** for the scan to complete.  You can also look in **Assessment runs** and check the **status**. Feel free to continue through this module and check the results later on." 

After review you should see that password authentication over SSH is configured on the instance. In addition, if you examine some of the other Inspector findings you will see that there are no password complexity restrictions. This means the instance is more susceptible to an SSH brute force attack. 

<!--
2.  Click on **securityhub default** under **Insight Groups**
3. Click **Manage** (in the upper right hand corner of the dashboard) and then click **Define Insight**
4.  We will now define the filters for the insight. Under "Findings" select **Provider** from the pull down menu. Next to that select **Inspector**. This will add **Provider: Inspector** to the filters. Next select **Keyword** from the pull down menu under findings (it should already be the default.) Next to that enter the following text `password authentication over SSH` then hit enter. You will have added a keyword filter. 
5. Click **Create insight** so we can save this insight for future use. Enter the following into insight name **`Instances allowing password authentication over SSH`** and toggle the **Display on insights page** so it is enabled then finally click **Ok**.
-->

**Determine if the attacker was able to login to the EC2 instance (CloudWatch logs)**

Now that we know that the instance was more susceptible to an SSH brute force attack, let’s look at the CloudWatch logs and create a metric to see if there were any successful SSH logins (to finally answer the question of whether the SSH brute force attack was successful.) Your corporate policy is to send security certain logs from EC2 instances to CloudWatch. 

1.  Go to <a href="https://us-west-2.console.aws.amazon.com/cloudwatch/home?region=us-west-2#logs:" target="_blank">CloudWatch logs</a>.
2.  Click on the log group **/threat-detection-wksp/var/log/secure**
3.  If you have multiple log streams, filter using the Instance ID you copied earlier and click on the stream.
4.  Within the **Filter Events** text box put the following Filter Pattern: **`[Mon, day, timestamp, ip, id, msg1= Invalid, msg2 = user, ...]`**

    !!! question "Do you see any failed (invalid user) attempts to log into the instance? Would that be consistent with an SSH brute force attack?"
    
5.  Now replace the Filter with one for successful attempts: **`[Mon, day, timestamp, ip, id, msg1= Accepted, msg2 = password, ...]`**

    !!! question "Do you see any successful attempts to log into the instance? Which linux user was compromised?"
    
### Respond

**Modify the EC2 security group (EC2)**

The active session from the attacker was automatically stopped by an update to the NACL on the subnet where the instance resides. This was done by a CloudWatch event rule trigger that is invoked based on certain GuardDuty findings. You've decided that all administration on EC2 Instances will be done through <a href="https://aws.amazon.com/systems-manager/" target="_blank">AWS Systems Manager</a> so you no longer need administrative ports open so a good next step would be to modify the security group associated with the EC2 instance to prevent the attacker or anyone else from connecting.

1.  Go to the <a href="https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2" target="_blank">Amazon EC2</a> Console.

2.  Find the running instances with the name **threat-detection-wksp: Compromised Instance**.

3.  Under the **Description** tab, click on the Security Group for the compromised instance.

4.  View the rules under the **Inbound** tab.

5.  Click **Edit** and delete the inbound SSH rule.

    !!! info "The SSM Agent was installed on your EC2 Instance during the initial configuration."
    
6. Click **Save**


<!-- ## Part 3 - Compromised S3 bucket

### Detect 

Now that we know the SSH brute force attack was successful and we disabled the IAM credentials that were stolen, we need to determine if anything else occurred. One step we could take here is to examine the IAM policy attached the IAM role that generated the temp credentials. We notice in the policy that there are permissions relating to the Amazon S3 service so that is something to keep in mind as you continue the investigation. 

Here is a truncated view of the policy from the IAM role attached to the compromised EC2 instance:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": "s3:PutObject",
            "Resource": "arn:aws:s3:::threat-detection-wksp-ACCOUNT_ID-us-west-2-gd-threatlist/*",
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:*"
            ],
            "Resource": "arn:aws:s3:::threat-detection-wksp-ACCOUNT_ID-us-west-2-data/*",
            "Effect": "Allow"
        },
        {
            "Action": [
                "s3:*"
            ],
            "Resource": "arn:aws:s3:::threat-detection-wksp-ACCOUNT_ID-us-west-2-data",
            "Effect": "Allow"
        }
    ]
}
```

<!-- **Investigate any S3 related findings (AWS Security Hub)**

There are many ways to approach this next step. We are going to start with a Security Hub insight that may be helpful in situations like this. This is not the only way you could approach this but it can definitely save time initially as you investigate the full repercussions of an attack.

1. Go to <a href="https://us-west-2.console.aws.amazon.com/securityhub/home?region=us-west-2#/insights" target="_blank">AWS Security Hub</a> in the AWS Management Console.
2. The link should take you to the **Insights** section (if not, click on ** Insights** in the navigation on the left).
3. Click in the **Filter insights** box and type **`Top S3`** which will display the built in Insight "Top S3 buckets by counts of findings." Click on that Insight. 
4. There should be one that with **threat-detection-wksp-** and ends in **-data**. Click on that. 
5. Evaluate the Macie findings shown under the Insight.

This **Security Hub** Insight is one way of determining what an attacker may have done. It is not going to help in every situation though. 
 
**Check if sensitive data was involved (Macie)**

At this point you know how the attacker was able to get into your systems and a general idea of what they did. In the previous step you  determined that the S3 bucket that starts with **threat-detection-wksp-** and ends in **-data** has an ACL that grants global read rights. We will now check if there is any sensitive and business-critical data in the bucket and take a closer at the Macie Alerts.

1. Go to the <a href="https://mt.us-west-2.macie.aws.amazon.com/" target="_blank">Amazon Macie</a> in the AWS Management console.

2.  Click **Dashboard** on the left navigation.  You should see the following data classifications:
    ![Macie Classification](/images/03-macie-data.png)

    !!! info "You can slide the risk slider to filter data classifications based on risk levels."

3. Above the risk slider, click the icon for **S3 public objects and buckets**. The icon will be in the shape of a globe but you can also hover over the icons to find the right one. 
    ![Public Objects Button](/images/03-macie-public-objects-button.png)

4. Click the magnifying glass to the left of the bucket name listed.
5. Check if any of the data in the bucket is considered a high risk.  Look for the **Object PII priority** field and **Object risk level** field.
    
6.  Verify if any of the data is unencrypted.  Look for the **Object encryption** field. 

    !!! question "Does a portion of the blue bar indicate that encryption is set to none?."
    
### Respond

**Fix the permissions and encryption on the bucket (S3)**

In the previous step we determined that the S3 bucket that starts with **threat-detection-wksp-** and ends in **-data** has sensitive data and some of that data is unencrypted. We also know that the bucket grants global read rights. We need to manually fix these issues. 

1. First we will fix the permissions.  Go to <a href="https://us-west-2.console.aws.amazon.com/s3/" target="_blank">Amazon S3</a> in the AWS Management Console. 	
3. Find the bucket that starts with **threat-detection-wksp-** and ends in **-data**
4. Click on the **Permissions** tab then click on **ACL Control List**
5. Under **Public access** click on the radio button next to **Everyone**. Uncheck **List objects** then click **Save**.
7. Now we need to fix the encryption.  In the same bucket, click on the **Properties** tab then click on **Default encryption**
8. Set the encryption to AWS-KMS. Select the **aws/s3** key. Finally click **Save**.

    !!! info "What impact does enabling default encryption have on existing objects in the bucket?"
-->