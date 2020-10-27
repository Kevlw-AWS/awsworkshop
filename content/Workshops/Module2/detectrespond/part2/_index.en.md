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

1. Go to the <a href="https://ap-southeast-2.console.aws.amazon.com/securityhub/home?region=ap-southeast-2#/findings" target="_blank">AWS Security Hub</a> console.
2. The link should take you to the **Findings** section (if not, click on **Findings** in the navigation on the left).
	* Add a filter by clicking in the **Add filter** box and scrolling down to **Product Name**, and paste in the word `GuardDuty`.

	* Use your browser's find function **Control-F** and paste in the `<Instance ID>` you copied earlier (from the principal ID you gathered in the GuardDuty finding). 

    * Now copy the <a href="https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html" target="_blank">Amazon Resource Name (ARN)</a> from the **Resource ID** for the first match. The ARN will look something like this `arn:aws:ec2:ap-southeast-2:166199753942:instance/i-0efc5172a5d7ecc6b`

    * Add one more filter by clicking the **Add filter** box again and selecting **Resource ID** and paste in the ARN from the previous step

{{% notice tip%}}
What GuardDuty findings do you see related to this instance ID?
{{% /notice %}}

One of the findings should indicate that the EC2 instance is communicating with an IP address on a threat list (**disallowed IP**) which adds further evidence to the conclusion that the instance has been compromised. The other finding should indicate that a system at a particular IP address is performing an SSH brute force attack against your instance.  You now need to investigate if the SSH brute force attack was successful and if that is what allowed the attacker to gain access to the instance.

<!-- **Determine if ssh password authentication is enabled on the EC2 instance (AWS Security Hub)**

Automated responses to threats can do many things. For example, you could have an trigger that helps gather information about the threat that could then be used in the investigation by the security team. With that option in mind, we have a CloudWatch event rule in place that will trigger an <a href="https://aws.amazon.com/inspector/" target="_blank">Amazon Inspector</a> scan of an EC2 instance when GuardDuty detects a particular attack. We will use AWS Security Hub to view the findings from Inspector. We want to determine if the SSH configuration adheres to best practices. 

1. Go to the <a href="https://ap-southeast-2.console.aws.amazon.com/securityhub/home?region=ap-southeast-2#/findings" target="_blank">AWS Security Hub</a> console.
2. The link should take you to the **Findings** section (if not, click on **Findings** in the navigation on the left). 
    * Add a filter by clicking in the **Add filter** box and scrolling down to **Product Name**, and paste in the word `Inspector`.
	* Use your browser's find function **Control-F** and paste in `password authentication over SSH`
    * The finding may not be on the first page of findings, use the `>` to move to the next page. -->

<!-- Click in the **Add filter** box:
* Scroll down to **Title**, change the operator to **CONTAINS** and paste in `password authentication over SSH`.
-->

<!-- Click on the finding regarding SSH and password authentication for the instance that experienced the SSH brute force attack and review. -->

<!--
1. Go to [AWS Security Hub](https://ap-southeast-2.console.aws.amazon.com/securityhub/) in the AWS Management Console.
2. On the left navigation, click on **Explore Findings**
3. Add the following filter:
	* **Keyword: `password authentication over SSH`** 
	* **Provider: Inspector**
4. In the results do you see a finding regarding SSH and password authentication for the instance that experienced the SSH brute force attack? 
-->

<!-- {{% notice info%}}
If you do not see any findings after a while, there may have been an issue with your Inspector agent.  Go to the <a href="https://ap-southeast-2.console.aws.amazon.com/inspector" target="_blank">Inspector</a> console, click on **Assessment Templates**, check the template that starts with **threat-detection-wksp**, and click **Run**.  Please allow **15 minutes** for the scan to complete.  You can also look in **Assessment runs** and check the **status**. Feel free to continue through this module and check the results later on.
{{% /notice %}}

After review you should see that password authentication over SSH is configured on the instance. In addition, if you examine some of the other Inspector findings you will see that there are no password complexity restrictions. This means the instance is more susceptible to an SSH brute force attack.  -->

**Determine if the attacker was able to login to the EC2 instance (CloudWatch logs)**

Now that we know that the instance was more susceptible to an SSH brute force attack, let’s look at the CloudWatch logs and create a metric to see if there were any successful SSH logins (to finally answer the question of whether the SSH brute force attack was successful.) Your corporate policy is to send security certain logs from EC2 instances to CloudWatch. 

1.  Go to <a href="https://ap-southeast-2.console.aws.amazon.com/cloudwatch/home?region=ap-southeast-2#logs:" target="_blank">CloudWatch logs</a>.
2.  Click on the log group **/threat-detection-wksp/var/log/secure**
3.  If you have multiple log streams, filter using the Instance ID you copied earlier and click on the stream.
4.  Within the **Filter Events** text box put the following Filter Pattern: **`[Mon, day, timestamp, ip, id, msg1= Invalid, msg2 = user, ...]`**

{{% notice tip%}}
Do you see any failed (invalid user) attempts to log into the instance? Would that be consistent with an SSH brute force attack?
{{% /notice %}}
    
1.  Now replace the Filter with one for successful attempts: **`[Mon, day, timestamp, ip, id, msg1= Accepted, msg2 = password, ...]`**

{{% notice tip%}}
Do you see any successful attempts to log into the instance? Which linux user was compromised?
{{% /notice %}}
    
### Respond

**Modify the EC2 security group (EC2)**

The active session from the attacker was automatically stopped by an update to the NACL on the subnet where the instance resides. This was done by a CloudWatch event rule trigger that is invoked based on certain GuardDuty findings. You've decided that all administration on EC2 Instances will be done through <a href="https://aws.amazon.com/systems-manager/" target="_blank">AWS Systems Manager</a> so you no longer need administrative ports open so a good next step would be to modify the security group associated with the EC2 instance to prevent the attacker or anyone else from connecting.

1.  Go to the <a href="https://ap-southeast-2.console.aws.amazon.com/ec2/v2/home?region=ap-southeast-2" target="_blank">Amazon EC2</a> Console.

2.  Find the running instances with the name **threat-detection-wksp: Compromised Instance**.

3.  Under the **Description** tab, click on the Security Group for the compromised instance.

4.  View the rules under the **Inbound** tab.

5.  Click **Edit** and delete the inbound SSH rule.

{{% notice tip%}}
The SSM Agent was installed on your EC2 Instance during the initial configuration.
{{% /notice %}}
    
1. Click **Save**