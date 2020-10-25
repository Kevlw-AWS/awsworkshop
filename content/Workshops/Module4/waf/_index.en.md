+++
title = "Web Application Firewall"
date = 2020-08-18T11:04:54-05:00
weight = 9
pre = "<b>4. </b>"
+++

1. Select the `WAF and Shield` service, and go to the `AWS WAF`.

 -----

 ###### ***TIP:***
 ***Check that the region in the URL is set to `us-west-2` when in the WAF console.***  It is sometimes set to a different region by using the navigation pane in the AWS Firewall Manager.

 -----

2. From the `AWS WAF` page, select `Web ACLs`.  Be sure to select in the filter the correct region: US-West (Oregon) `us-west-2`.

3. Select the `PCIWAF` and then the "Associated AWS Resources" tab.

4. Click the "Add AWS Resources" button. From the pop-up box, select application load balancer as the resource type and then the Web resource.  Select Add to close.
