+++
title = "Security Groups"
date = 2020-08-18T11:04:54-05:00
weight = 10
pre = "<b>5. </b>"
+++

Finally, *Requirement 1.1* of the PCI DSS v3.2.1 standards requires that a firewall that controls access to and between systems on the internal and external network be maintained and that the surface area availble to attack is minimised to only the necesarry ports for the application to function.

Protecting our EC2 instances are a number of network controls.  We're going to focus on [Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) which act as a virtual firewall, controlling inboudn and outbound traffic to our instances.

1. Start by heading to the [Security Groups](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#SecurityGroups:) console

2. Inspect the groups that have been created.  Look at the rules defined and how permissive they are.

![EC2 Security Group Before](/images/04-pci-ec2-sg1.png)

{{% notice note %}}
What type of traffic would these groups allow for right now?
{{% /notice %}}

Let's modify one Security group tegether then you can adjust the rest.

3. Select the `jump-sg` group and click on **Edit inbound rules**

4. Delete the current rule

5. Create a new rule to allow SSH (Port 22) from anywhere

![EC2 Security Group After](/images/04-pci-ec2-sg2.png)

6. Click Save rules to commit the changes

Now modify the following Security groups to match the new, more restrictive rule-set

Group | Application (Port) | Direction | Source
----- | ----- | ----- | -----
jump-sg | SSH (22) | Inbound rule | Anywhere (0.0.0.0/0)
dbhost-sg | MYSQL (3306) | Inbound rule | apphostSG
webhost-sg | HTTP (80) <br/> HTTPS (443) | Inbound rule | albSG
apphost-sg | HTTP (80) <br/> HTTPS (443) | Inbound rule | webhostSG

We have now configured our Security groups to minimise our exposure, lets go ahead and [test our solution](./review.html) next and review what we did.