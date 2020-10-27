+++
title = "Lab 6: Sleeper Agent"
date = 2019-11-18T08:23:04+11:00
weight = 30
chapter = false
+++

In this workshop you'll learn how you can detect a sleeper agent who has compromised your  AWS account!

 Luckily you were alerted and able to evict the attacker quickly, or so you thought. The attacker seems to have a mysterious way of getting back into your account no matter what you do, can you stop him? What can you do to prevent, detect, and respond to such incidents in the future?

### Lab Overview

 {{< rawhtml >}}
<video width="696" height="392" controls>
  <source src="https://apj-security-workshop.s3-ap-southeast-2.amazonaws.com/q4/lab6-intro-sourced.mp4" type="video/mp4">
  Your browser doesn't support video.
</video>
{{< /rawhtml >}}

>  **Speakers: Jem Richards, CTO** 

>  *In this video, you’ll also hear from our partner [RedBear IT](https://a.mzn.cloud/jam-redbearit) discussing the workshop you'll undertake, the AWS services you'll explore and highlighting a real-world example of the deployment of the AWS services you’ll use. For more information, please visit [RedBear IT](https://a.mzn.cloud/jam-redbearit)*

{{% notice warning %}}
Your AWS account was compromised!! Luckily you were alerted and able to evict the attacker quickly, or so you thought. The attacker seems to have a mysterious way of getting back into your account no matter what you do, can you stop him? What can you do to prevent, detect, and respond to such incidents in the future?
{{% /notice %}}


### Background
 
An attacker got hold of a pair of access/secret keys from Github and got into your AWS account. GuardDuty detected the intrusion and raised an unauthorized credential exfiltration alert. The compromised credentials were quickly identified. You immediately deactivated the stolen keys and disabled the compromised account. Breathing a sigh of relief, you felt like you fought off this attack.
A few days later after a new user was created, you were woken up to another GuardDuty alert. The attacker is back!! You went through the same motions to evict the attacker, but started to have a bad feeling about this.


### Lab Steps
{{% children depth=3 %}}