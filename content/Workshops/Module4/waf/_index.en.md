+++
title = "Web Application Firewall"
date = 2020-08-18T11:04:54-05:00
weight = 9
pre = "<b>4. </b>"
+++

PCI DSS v3.2.1 through Requirement 6.6 establishes the need for public-facing web applicaitons to be protected from new threats and vulnerabilities on an ongoing basis as well as assuring that applications are protected against known attacks.  [AWS WAF- Web Application Firewall](https://aws.amazon.com/waf/) helps meet this requirement by protecting your web applications or APIs against common web exploits.

In this section we're going to protect an Application Load Balancer against common exploits using AWS WAF.

1. Open the [WAF & Shield](https://console.aws.amazon.com/wafv2/homev2#) console
   
2. From the left hand navigation select Web ACLs

{{% notice warning %}}
***Check that the region in the dropdown is set to `Oregon` when in the Web ACLs console.*** This may default to a different region on first load.
{{% /notice %}}

![WAF Region](/images/04-pci-waf-region.png)

3. We have one ACL defined: `PCIWAFV2`, select this ACL to view its details
   
4. Go ahead and explore this ACL, does it have any rules defined?
   
5. Select the **Associated AWS resources** tab
   
6. Click on **Add AWS resources** to add our ACL to a load balancer that has been created for you
   
7.  Select the **Application Load Balancer** option and then select `mod-m-rWebH-...`

8. Click **Add** to associate this ACL with the load balancer

![WAF ACL](/images/04-pci-waf-acl.png)

### Bonus

9. Head to the **Rules** tab and see if you can an **AWS managed rule** to protect against `Known bad inputs`

Your rules should like this when done

![WAF Rules](/images/04-pci-waf-rule.png)

10. Head back to the **Overview** tab and you should see new CloudWatch metrics for your ACL; they won't populate with data as we don't have any traffic

![WAF Metrics](/images/04-pci-waf-metrics.png)

With our WAF ACLs in place it's time to head to our final task to lock down our [Security Groups](./ec2.html) protecting our EC2 instances.