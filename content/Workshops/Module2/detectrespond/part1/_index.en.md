+++
title = "Compromised AWS IAM credentials"
menuTitle = "Compromised IAM credentials"
date = 2020-07-30T11:30:52-05:00
weight = 1
pre = "<b> </b>"
+++

### Detect and investigate 

By now you’ve received email alerts from the security services you enabled. Now what? As part of your risk driven detection strategy your organization has decided to prioritize AWS IAM related findings.  

1. Sort through your email alerts and identity an alert related to an AWS IAM principal

{{% notice info%}}
Amazon GuardDuty Finding: UnauthorizedAccess:IAMUser/MaliciousIPCaller.Custom
{{% /notice %}}
	
1. Copy the `<Access Key ID>` from the e-mail alert. 

**Explore findings related to the access key (Amazon GuardDuty)**

Now that you have a resource identifier to pivot from you can use Amazon GuardDuty to start doing an initial investigation into these findings.

1. Go to the <a href="https://ap-southeast-2.console.aws.amazon.com/guardduty/" target="_blank">Amazon GuardDuty</a> console (ap-southeast-2).

2. Click in the **Add filter criteria** box, select **Access Key ID**, and then paste in the `<Access Key ID>` you copied from the e-mail, then select **Apply**.

{{% notice tip%}}
What findings do you see related to this Access Key ID?
{{% /notice %}}
	
3. Click on one of the findings to see the details.

{{% notice tip%}}
What principal are these credentials associated with?
{{% /notice %}}

1. Examining **Iam instance profile** under **Resource affected** you can see that the access key referenced in this finding is from an IAM assumed role. 

2. Examining **Iam instance profile** under **Resource affected** you will find two strings separated by a new line. The first is the <a href="https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html" target="_blank">Amazon Resource Name (ARN)</a> of the IAM role that was compromised. The second line will be the  <a href="https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-unique-ids" target="_blank">unique ID</a> for the IAM role. 

{{% notice info%}}
You may have to resize your screen by dragging the middle vertical scrollbar to the left to see the entire text
{{% /notice %}}

1. The **Iam instance profile** contains a unique ID for the entity making the API request, and when the request is made using temporary security credentials (which is what happens for an assume role call) it also includes a session name. In this case the session name is the EC2 instance ID since the assume role call was done using an IAM role for EC2.

2. Copy the full **Iam instance profile** which contains both the unique ID of the role and the IAM Role ARN: 
**"Iam instance profile": "
`< ARN>`
 `<unique ID >`"**

8. Examine the **Iam instance profile** under **Resource affected** and copy it down. This corresponds to the name of the IAM role involved since the temp creds used to make the API call came from EC2 instance with an IAM role attached. 

<!--

To use SH for this we could use the insight "AWS users with the most suspicious activity" but that would be a stretch - no way to take this and figure out an IAM role is involved just by using the SH console.


1. Go to the [AWS Security Hub](https://ap-southeast-2.console.aws.amazon.com/securityhub/home?region=ap-southeast-2#/investigate) console.
2. The link should take you to the **Investigate** section but if not, click on **Investigate** in the navigation on the left.
3. Click in the **Add filter** box:

	* Scroll down to **Severity Label**, change the operator to **EQUALS** and type in **MEDIUM**
	
	* Use your browser's find function **Control-F** and paste in the `<Access Key ID>` you copied from the e-mail. 

	>  What findings do you see related to this access-key ID?
	
4. Click on one of the findings to see the details.

	> Where did these credentials come from? 

Examining **userType** under **Resource details**/**Details** you can see that the access key referenced in this finding is from an IAM assumed role. Examining **principalID** under **Details** you will find two strings separated by a colon. The first is the [unique ID](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_identifiers.html#identifiers-unique-ids) for the role and the second is the EC2 instance ID. The **principalID** contains a unique ID for the entity making the API request, and when the request is made using temporary security credentials (which is what happens for an assume role call) it also includes a session name. In this case the session name is the EC2 instance ID  since the assume role call was done using an IAM role for EC2.

5. Copy the full **principalId** which contains both the unique ID of the role and the session name
	* **"principalId": "`< unique ID >:< session name >`"**

6. Click **Cancel** (upper right-hand corner) to return back to the findings and paste only the **unique ID** into the filter:
	* **Keyword: `<unique ID>`**

Filtering on the access key ID like you did previously earlier will only show you findings related to that specific access key.  In this case the access key is from an assumed role call which means it will change over time.  Rather than using the access key id you can filter on the unique ID for the AWS IAM role which will show you all findings related to any access keys generated by that AWS IAM role.
	
7. After you have applied the filter check all the checkboxes for the findings, click **Actions**, and set active status to **In Progress** (since we are actively investigating this.)

8. Click **Create Insight** so you can further track findings related to this IAM principal.  Enter the following into insight name **`Show me findings related to <Unique ID>`** and toggle the **Display on insights page** so it is enabled and click **Ok**

-->

### Respond

Now that you have identified that a temporary security credential from an IAM role for EC2 is being used by an attacker, the decision has been made to rotate the credential immediately to prevent any further misuse or potential privilege escalation.
  
**Revoke the IAM role sessions (IAM)**

1.  Browse to the <a href="https://console.aws.amazon.com/iam/home?region=ap-southeast-2" target="_blank">AWS IAM</a> console.

2.  Click **Roles** and find the role you identified in the previous section using the **User Name** you copied down earlier (this is the role attached to the compromised instance), and click on that **Role Name**.

3.  Click on the **Revoke sessions** tab.

4.  Click on **Revoke active sessions**.

5.  Click the acknowledgement **check box** and then click **Revoke active sessions**. 

    !!! question "What is the mechanism that is put in place by this step to actually prevent the use of the temporary security credentials issued by this role?"

**Restart the EC2 instance to rotate the access keys (EC2)**

All active credentials for the compromised IAM role have been invalidated.  This means the attacker can no longer use those access keys, but it also means that any applications that use this role can't as well.  You knew this going in but decided it was necessary due to the high risk of a compromised IAM access key. In order to ensure the availability of your application you need to refresh the access keys on the instance by stopping and starting the instance. *A simple reboot will not change the keys.* If you waited the temporary security credential on the instance would be refreshed but this procedure will speed things up. Since you are using AWS Systems Manager for administration on your EC2 instances you can use it to query the metadata to validate that the access keys were rotated after the instance restart.

6. In the <a href="https://ap-southeast-2.console.aws.amazon.com/ec2/v2/home?region=ap-southeast-2#Instances:sort=instanceId" target="_blank">EC2 console</a> **Stop** the Instance named **threat-detection-wksp: Compromised Instance**.

Check the box next to the instance, select the **Actions menu**, **Instance State**, **Stop**, confirm by pressing **Yes**, **Stop**

7. Wait for the Instance State to say **stopped** under **Instance State** (you may need to refresh the EC2 console) and then **Start** the instance.

    !!! info "You will need to wait until all Status Checks have passed before continuing."

**Verify the access keys have been rotated (Systems Manager)**

8.  Go to <a href="https://ap-southeast-2.console.aws.amazon.com/systems-manager/session-manager?region=ap-southeast-2" target="_blank">AWS Systems Manager</a> console and click on **Session Manager** on the left navigation and then click **Start Session**.  

    You should see an instance named **threat-detection-wksp: Compromised Instance** with a **Instance state** of **running**.
    
9.  To see the credentials currently active on the instance, click on the radio button next to **threat-detection-wksp: Compromised Instance** and click **Start Session**.

11.	Run the following command in the shell and compare the access key ID to the one found in the email alerts to ensure it has changed:
	
``` bash
curl http://169.254.169.254/latest/meta-data/iam/security-credentials/threat-detection-wksp-compromised-ec2
```

!!! question "Why would this scenario be a good use case for auto-scaling groups?" 

At this point you've successfully revoked all the active sessions from AWS IAM role and rotated the temporary security credentials on the EC2 instance.

<!--
, and created an AWS Security Hub insight to allow you to continue to track findings related to the role.  You can view the insight you created by clicking on **Security Hub default** in the AWS Security Hub console.
-->
