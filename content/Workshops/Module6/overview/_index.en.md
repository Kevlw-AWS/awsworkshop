+++
title = "Overview"
menuTitle = "Overview"
date = 2020-07-30T11:04:54-05:00
weight = 5
pre = "<b>1. </b>"
+++

{{% notice note %}}
This workshop is available in the follow region:   
**`us-east-1 (N. Virginia)`**  
{{% /notice %}}

## Background

An attacker got hold of a pair of access/secret keys from Github and got into your AWS account.  GuardDuty detected the intrusion and raised an unauthorized credential exfiltration alert.  The compromised credentials were quickly identified.  You immediately deactivated the stolen keys and disabled the compromised account.  Breathing a sigh of relief, you felt like you fought off this attack.

A few days later after a new user was created, you were woken up to another GuardDuty alert.  The attacker is back!!  You went through the same motions to evict the attacker, but started to have a bad feeling about this.  

#### Your mission
How could the attacker come back again so quickly?  He must have planted a backdoor somewhere in your account, but where?  You have to find the backdoor to stop him from coming back again.  You also want to set up an alert to be notified of activity that could lead to this in the future. 

**Good starting points:**<p>
</p><ul><li>There is a URL presented within output parameters that will provide you an update on your status in completing this challenge.
  <p></p></li><li>Think about all the ways an attacker can get back to the account - IAM users, overly-permissive assumable role, faulty lambda functions, compromised EC2 instances, misconfigured WAF, instance profiles.
  <p></p></li><li>Long-term persistent credentials (access/secret key, login id/password) are the easiest way for an attacker to get into the door.
  <p></p></li><li>Use CloudWatch to detect privileged IAM operations, especially operations that creates long-term credentials automatically by a lambda function.
  
{{% notice warning %}}
The CloudWatch rule should only monitor the **specific** privileged IAM operations
{{% /notice %}}
  
  </li></ul>

To solve this challenge, you must remove the method that is being used to access the account and properly setup an alert to notify you of suspicious activity that could lead to this problem in the future.
