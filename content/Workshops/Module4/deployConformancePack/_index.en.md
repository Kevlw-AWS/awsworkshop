+++
title = "Deploy Conformance Pack"
menuTitle = "Deploy Conformance Pack"
date = 2020-08-18T14:27:09-05:00
weight = 25
pre = "<b>5. </b>"
+++

#### 1. Deploy your updated conformance pack
1. Go to the [AWS Config](https://console.aws.amazon.com/config/home) console.
2. Select **Conformance Packs** from the left navigation menu
3. Select **Deploy conformance pack**
![Conformance packs](../../../images/04-conformance-packs.png)

3. Under Templete details, select **Template is ready** 
4. Under Template location, select **Upload a template file**
5. Select the **Chose file** button  
6. Select the ***s3-best-practices-with-remediation-pack.yaml*** (file from step above)
7. Select the **Next** button 
8. Enter a **Conformance pack name** something like *“S3-conformance-pack”* makes sense but you can name it whatever you like.
9. **Select S3 bucket**
10. Select the S3 bucket named **awsconfigconforms-delivery-bucket-*{YOUR-AWS-ACCOUNT-ID}***. *This bucket was created as part of prerequisite cloudformation template in previous section.*
![Specify conformance pack details](../../../images/04-conformance-pack-specify-conformance-details.png)
11. Under parameter, click on **Add Parameter**. 
12. Enter the Key as **S3TargetBucketNameForEnableLogging** 
12. Enter the Parameter Value as **s3serversideloggingbucket-*{YOUR-AWS-ACCOUNT-ID}*** (*Ensure do not include any dashes in your account ID*) 
13. Select the **Next** button
14. Select the **Deploy conformance pack** button

![Specify conformance pack details](../../../images/04-conformance-pack-deployed.png)

17. Deploying the Conformance Pack may take a few minutes. 

You can now progress to the next step 