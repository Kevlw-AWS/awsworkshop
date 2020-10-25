+++
title = "Introduction"
date = 2020-08-18T11:04:54-05:00
weight = 5
pre = "<b>0. </b>"
+++

{{% notice note %}}
This workshop is available in the follow region:  
**`us-west-2 (Oregon)`**  
{{% /notice %}}


### Summary
Re-architect your AWS environment to meet PCI DSS compliance.

### Background

You are the new cloud security and compliance engineer who has just joined a major online retailer. Their sales have been increasing dramatically year over year, and they are transitioning their online presence to the cloud. The increase in annual transactions means they now must also demonstrate compliance with the Payment Card Industry Data Security Standard (PCI DSS).

A junior engineer has architected an environment within AWS. Using your AWS expertise, you must go in to ensure that the deployment aligns with the PCI DSS requirements before additional resources are added.

A multi-tier environment has been provided with subnets in different availability zones. There's a subnet for a jump server to manage resources, a web and application layer subnet, and a backend database subnet.

The web application subnet is front-ended by an Internet facing application load balancer, and CloudTrail event logging is enabled.

### Challenge

As the AWS security and compliance expert, you are tasked with reviewing and remediation of the deployed architecture.

Review the IAM security policy under account settings to ensure that it aligns with the PCI DSS requirements.

The deployment is in `us-west-2`, and you need to associate the `PCIWAF` with the available load balancer.

{{% notice tip %}}
***Check that the region in the URL is set to `us-west-2` when in the WAF console.***  It is sometimes set to a different region by using the navigation pane in the AWS Firewall Manager.
{{% /notice %}}

CloudTrail has been enabled for you, but you will need to identify the S3 bucket used to store the trail activity and ensure encryption has been enabled on it.

A customer managed encryption key `CMK` has also been created called `PCIEncryptionKey`. It should be configured for annual rotation.

There are multiple subnets that have associated security groups, but their access is very open. The security groups need to be configured to restrict communications for approved ports.

The web and application security groups should only allow inbound communications over ports `80` and `443`.

The `jumpserver` security group should only allow inbound access over port `22`.

`MySQL` will be temporarily deployed as the backend database before you move to a managed `RDS` solution, in the meantime, the database security group should only allow inbound access over port `3306`.
