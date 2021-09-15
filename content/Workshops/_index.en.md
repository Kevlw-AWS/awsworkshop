+++
title = "Workshops"
date = 2019-11-18T08:29:21+11:00
weight = 3
chapter = false
disableToc = "false"
+++

## Workshops

These workshops are designed to help you get familiar with AWS Security and Operational services so you can improve your security and compliance objectives. 

* You will be implementing these steps within your own AWS account. Therefore, access to implement these security controls within your AWS environment is mandatory.
* Follow the instructions in the workshop as you make your way through these Top 10 steps. 
* You will be given 2 hours to implement these controls within your account. 
* You can reach out to our AWS solutions architects if you experience an issue with the implementation of any of these controls. 

| Topic | Description |
|-----------|---------|
|[1. Accurate Account Info](/workshops/module1) | When AWS needs to contact you about your AWS account (https://aws.amazon.com/answers/security/aws-secure-account-setup/), we use the contact information defined in the AWS Management Console, including the email address used to create the account and those listed under Alternate Contacts. You should also have a process for regularly checking that these email addresses work, and that you are responding to emails—especially security notifications you might receive from abuse@amazon.com.
|[2. Use MFA](/workshops/module2)| MFA is the best way to protect accounts from inappropriate access. Always set up MFA on your Root user and AWS Identity and Access Management (IAM) users. If you use AWS Single Sign-On (SSO) (https://aws.amazon.com/single-sign-on/) to control access to AWS or to federate your corporate identity store, you can enforce MFA there. Implementing MFA at the federated identity provider (IdP) means that you can take advantage of existing MFA processes in your organization. 
|[3. No Hardcoding Secrets](/workshops/module3)| When you build applications on AWS, you can use AWS IAM roles to deliver temporary, short-lived credentials for calling AWS services. However, some applications require longer-lived credentials, such as database passwords or other API keys. If this is the case, you should never hard code these secrets in the application or store them in source code.
|[4. Limit Security Groups](/workshops/module4)| Security groups are a key way that you can enable network access to resources you have provisioned on AWS. Ensuring that only the required ports are open and the connection is enabled from known network ranges is a foundational approach to security.
|[5. Intentional Data Policies](/workshops/module5)| Not all data is created equal, which means [classifying data properly is crucial to its security](https://aws.amazon.com/blogs/database/best-practices-for-securing-sensitive-data-in-aws-data-stores/). It’s important to accommodate the complex tradeoffs between a strict security posture and a flexible agile environment. 
|[6. Centralise CloudTrail Logs](/workshops/module6)| Logging and monitoring are important parts of a robust security plan. Being able to investigate unexpected changes in your environment or perform analysis to iterate on your security posture relies on having access to data
|[7. Validate IAM roles](/workshops/module7)| As you operate your AWS accounts to iterate and build capability, you may end up creating multiple IAM roles that you discover later you don’t need. Use [AWS IAM Access Analyzer](https://aws.amazon.com/iam/features/analyze-access/) to review access to your internal AWS resources and determine where you have shared access outside your AWS accounts. If you have already created multiple roles, you can [search for unused IAM roles](https://aws.amazon.com/blogs/security/continuously-monitor-unused-iam-roles-aws-config/) and remove them.
|[8. Take Action on GuardDuty findings](/workshops/module8)| [AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html), [Amazon GuardDuty](https://aws.amazon.com/guardduty/), and [AWS Identity and Access Management Access Analyzer](https://aws.amazon.com/iam/features/analyze-access/) are managed AWS services that provide you with actionable findings in your AWS accounts. 
|[9. Rotate your Credentials](/workshops/module9)| One of AWS Security Best Practices is to look for IAM users with access keys more than 90 days old. If you need to use access keys rather than roles, you should rotate them regularly.
|[10. Be involved in the Dev Cycle](/workshops/module10)| All of the guidance to this point has been focused on the technology configuration that you can implement. The last piece of advice, “be involved in the dev cycle,” is about people, and can be broadly summarized as “raise the security culture of your organization.” 