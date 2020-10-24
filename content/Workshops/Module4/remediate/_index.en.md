+++
title = "View Compliance and Remediation"
menuTitle = "View Compliance and Remediation"
date = 2020-08-18T14:27:09-05:00
weight = 30
pre = "<b>5. </b>"
+++

We will check compliance status for each rule in conformance pack and associated resources

1. Once conformance pack is deployed (*Previous step*)
2. Select the *Conformance pack name* to drill down into details.
3. You can now view a list of the rules and their compliance conformance status 
![Conformance pack rules](../../../images/04-config-conformance-pack-rules.png)
4. Click on a rules name to see the rule details
![S3 Bucket Public Write Prohibited](../../../images/04-config-S3BucketPublicWriteProhibited.png)
5. Expand Resources in Scope section to see resources in scope and their compliance status. 
6. If there are any existing non-compliant resources, you can manually remediate them or wait for auto-remediation to kick in.
7. (Optional) *To see auto-remediation in action on a new resource, create a new s3 bucket using S3 Console. AWS Config will discover the resource and mark it as non-compliant if it is not following S3 Best Practices.*
8. Go back to Conformance Pack details and select a rule with remediation action.
9. Expand Resources in Scope section to see newly created resource with its compliance status. 
- If the resource is non-compliant, auto-remediation action will apply to resource within few minutes.
10. **Refresh the page** to see updated resource compliance status.
11. You can also manually remediate a resource by selecting resource and clicking Remediate.
12. Take some time to explore the rest of the Config pages and dashboards outside of conformance packs.