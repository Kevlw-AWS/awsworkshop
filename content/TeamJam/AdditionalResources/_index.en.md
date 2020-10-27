+++
title = "Additional Resources"
date = 2019-11-18T08:26:11+11:00
weight = 1
chapter = false
+++

Curious on what you need to know for next time? This list of resources should have you sorted!

* Feline takeover
    * [Using versioning](https://docs.aws.amazon.com/AmazonS3/latest/dev/Versioning.html) in the Amazon Simple Storage Service documentation
* Privilege separation - got root?
    * Understand different types of policies in [Policies and permissions in IAM>](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html) from the AWS Identity and Access Management documentation
    * [How can I use permissions boundaries to limit the scope of IAM users and roles and prevent privilege escalation?](https://aws.amazon.com/premiumsupport/knowledge-center/iam-permission-boundaries/) from AWS support
    * Get hands on with [IAM permission boundaries delegation creation](https://wellarchitectedlabs.com/security/300_labs/300_iam_permission_boundaries_delegating_role_creation/) in the [AWS Well-Architected Labs](https://wellarchitectedlabs.com/)
* Self-service secured cloud
    * Read more about [AWS Service Catalog](https://aws.amazon.com/servicecatalog/)
    * Understand [launch constraints](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/constraints-launch.html)
    * Read how you can us a [TagOption Library](https://docs.aws.amazon.com/servicecatalog/latest/adminguide/tagoptions.html) to enforce tagging in Service Catalog
    * Get hands on with [AWS Service Catalog tools workshops](https://service-catalog-tools-workshop.com/)
* Perfect world
    * See the documentation for [modify_instance_attribute](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/ec2.html#instance) in the boto3 documentation.
* You can't secure what you can't see
    * Understand the [AWS Security Finding Format (ASFF)](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings-format.html) used for creating your own custom findings
    * Read an example custom finding on the AWS Security Blog in the post [Integrating AWS CloudFormation security tests with AWS Security Hub and AWS CodeBuild reports](https://aws.amazon.com/blogs/security/integrating-aws-cloudformation-security-tests-with-aws-security-hub-and-aws-codebuild-reports/)
    * See the documentation on [sending findings to a custom action](https://docs.aws.amazon.com/securityhub/latest/userguide/finding-send-to-custom-action.html)
    * Read the AWS Partner Blog on [How to Enable Custom Actions in AWS Security Hub](https://aws.amazon.com/blogs/apn/how-to-enable-custom-actions-in-aws-security-hub/)
* Secure your patient data
    * Read about [protecting data using server-side encryption](https://docs.aws.amazon.com/AmazonS3/latest/dev/serv-side-encryption.html) in the Amazon S3 documentation
    * Understand [configuring Amazon S3 event notifications](https://docs.aws.amazon.com/AmazonS3/latest/dev/NotificationHowTo.html)
    * Learn more about [VPC flow logs](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html)
    * See the documentation on [using Amazon CloudWatch alarms](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)
* Fix the KMS key
    * Read through [understanding key policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html) in the AWS Key Management Service documentation. In particular make sure you're familiar with [Allowing users in other accounts to use a CMK](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-modifying-external-accounts.html)
    * Understand the different [policies and permissions in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html), and how they intersect to provide access to AWS resources
* Least privilege put to the test
    * Read more on [permissions for IAM users to pass a role](https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs-cwl.html#flow-logs-iam-user) needed for VPC flow logs to write to CloudWatch
* Automated compliance for the win
    * Review the [AWS Config managed rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_use-managed-rules.html)
    * Understand how to create [AWS config custom rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules.html)
    * See the Amazon RDS documentation on [encryption Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html)
* Tag you're it
    * See the AWS IAM documentation on [What is ABAC for AWS?](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_attribute-based-access-control.html)
    * Follow the tutorial to [define permissions to access AWS resources based on tags](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_attribute-based-access-control.html)
    * Watch the AWS re:Invent breakout session [Access control confidence: Right access to the right things](https://www.youtube.com/watch?v=XO4CALyzbVM)

