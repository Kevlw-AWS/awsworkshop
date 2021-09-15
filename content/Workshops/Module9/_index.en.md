+++
title = "9. Rotate your Credentials "
date = 2019-11-18T08:23:04+11:00
weight = 30
chapter = false
+++

One of AWS Security Best Practices is to look for IAM users with access keys more than 90 days old. If you need to use access keys rather than roles, you should rotate them regularly. Review [best practices for managing AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html) for more guidance. If your users access AWS via federation, then [you can remove the need to issue AWS access keys for your users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_enable-console-saml.html). Users authenticate to the IdP and assume an IAM role in the target AWS account. The result is that long-term credentials are not needed, and your user will have short-term credentials associated with an IAM role.

In this exercise we will use AWS IAM Roles to avoid the usage of AWS IAM access keys that may be required by the Amazon Elastic Compute Cloud (EC2) instance to access AWS resources. We will create a Role and assigned it to EC2 instance, instead of hard coding the access keys within the EC2 instance.

Note: For this lab, it is assumed that EC2 instance is already created with default settings. For instructions to create EC2 Instance please follow the [link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/launching-instance.html).

1. From the AWS console, select *AWS Identity and Access Management*. 
2. To avoid the access key usage we first need to create an IAM role. Click on *Roles* on the menu on the left side of the console under Access Management.
3. Click on *Create role*.
4. Click on *AWS service*. Then click on *EC2* under ‘Choose a use case’ section.
![Select EC2](/images/Module-9-Image-1.png)

5. Click Next: Permission.
6. In the Search field type the policy that you want to attach to your EC2 instance and select from the list below i.e., AmazonRekognitionReadOnlyAccess policy.
![Select the AmazonRekognitionReadOnlyAccess policy](/images/Module-9-Image-2.png)

7. Click Next: Tags.
8. Provide the optional Key and value to the tag.
9. Click Next: Review
10. Provide a meaningful name for the Role and optional description. Click Create role.

![Create role](/images/Module-9-Image-3.png)

11. You will notice the newly created role is now appearing in the list of roles.
12. Go to services, click EC2.
13. On the dashboard, click on Instances (running). We will create a Role and assign it to the EC2 instance, instead of hard coding the access keys within the EC2 instance.
14. Select your EC2 instance that you want to assigned the role. Click Actions -> Security -> Modify IAM role.
![Modify IAM role](/images/Module-9-Image-4.png)
15. From the drop-down list of IAM roles, select the role that you have created in the previous steps.
16. Click Save. Your EC2 instance can now access the required AWS service with minimum privilege.

For more information please read the [AWS User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)