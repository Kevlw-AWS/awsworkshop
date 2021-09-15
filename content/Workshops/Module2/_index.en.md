+++
title = "2. Use MFA"
date = 2019-11-18T08:23:04+11:00
weight = 28
+++

MFA is the best way to protect accounts from inappropriate access. Always set up MFA on your Root user and AWS Identity and Access Management (IAM) users. If you use [AWS Single Sign-On (SSO)](https://aws.amazon.com/single-sign-on/) to control access to AWS or to federate your corporate identity store, you can enforce MFA there. Implementing MFA at the federated identity provider (IdP) means that you can take advantage of existing MFA processes in your organization. 

In this exercise we will use AWS Identity & Access Management (IAM) in the AWS Management Console to configure and enable a virtual multi factor authentication (MFA) device for both the *root account* as well as *IAM users*. 

Please note: To manage MFA devices for the AWS account, you must be signed in to AWS using your root user credentials. You cannot manage MFA devices for the root user using other credentials.

### Lab Steps
{{% children depth=1 %}}