+++
title = "4. Limit Security Groups"
date = 2019-11-18T08:23:04+11:00
weight = 30
chapter = false
+++

Security groups are a key way that you can enable network access to resources you have provisioned on AWS. Ensuring that only the required ports are open and the connection is enabled from known network ranges is a foundational approach to security. 

In this exercise we will use AWS Trusted Advisor’s basic security checks to identify remote access risks associated with the EC2 instance and fix them.

### Steps

1. From the AWS console, click *Services* and select *Trusted Advisor*.
2. You will notice that there are few risks identified by Trusted Advisor. Click on Security tab. You will notice findings for security groups about open network access. Now let’s fix these issues.

![Fix these issues](/images/Module-4-Image-1.png)

3. Click on one of the Security Group findings, which expand with more details. You will also see the list of security group names that have this particular security issue. .

![Click on Security Group findings](/images/Module-4-Image-2.png)

4. Click on the Security Group Name in the list. It will open a Security Group console on a new browser tab.

![Click on Security Group name](/images/Module-4-Image-3.png)

5. On Security Groups page, click on the Inbound rules. You will notice that there is one rule allowing open access to port 3389 from the internet, which is not a good practice. Therefore, we need to remove this rule.

![Remove the rule](/images/Module-4-Image-4.png)

6. Click on Edit inbound rules.

7. Click Delete associated with the open port of 3389. Click Save rules, which will remove the rule permanently.

![Click delete](/images/Module-4-Image-5.png)
8. Now go back to Trusted Advisor tab and click on the Refresh this check icon associated with the security risk.
9. Trusted Advisor will re-run the check and will show green once it finds that the issue is fixed.