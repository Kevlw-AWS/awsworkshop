+++
title = "Scenario"
date = 2020-08-18T11:43:23-05:00
weight = 6
pre = "<b></b>"
+++

You are the new cloud security and compliance engineer who has just joined a major online retailer. Their sales have been increasing dramatically year over year, and they are transitioning their online presence to the cloud. The increase in annual transactions means they now must also demonstrate compliance with the Payment Card Industry Data Security Standard (PCI DSS).

A junior engineer has architected an environment within AWS. Using your AWS expertise, you must go in to ensure that the deployment aligns with the PCI DSS requirements before additional resources are added.

A multi-tier environment has been provided with subnets in different availability zones. There's a subnet for a jump server to manage resources, a web and application layer subnet, and a backend database subnet.

The web application subnet is front-ended by an Internet facing application load balancer, and CloudTrail event logging is enabled.