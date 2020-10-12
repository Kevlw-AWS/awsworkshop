+++
title = "Create the first Data Classification Job"
date = 2020-07-30T15:09:09-05:00
weight = 15
chapter = true
pre = "<b></b>"
+++

Now we are going to create a Data Classification job so we can evaluate the contents of our S3 buckets.  The first job we create will run once a day and evaluate the complete contents of our S3 buckets to make sure we have correctly tagged and classified all our data.  This job will use only the managed identifiers available with Amazon Macie, the complete list of managed identifiers is available [here](https://docs.aws.amazon.com/macie/latest/user/managed-data-identifiers.html).

1. Go to the [Macie console](https://console.aws.amazon.com/macie/home).
2. To begin, select the **S3 buckets** option in the left hand menu.
3. Select the three S3 buckets labeled.  You may need to wait a minute and then click ***Refresh icon*** if all the buckets names do not display.
- macieworkshop-env-setup-publicbucket-\<random\>
- macieworkshop-env-setup-internalbucket-\<random\>
- macieworkshop-env-setup-confidentialbucket-\<random\>

4. Click on the **Create job** button. 
{{% notice note %}}
You are now able to verify the S3 buckets you chose before you continue, use the **Previous** or **Remove** buttons if you selected the incorrect S3 buckets.  
{{% /notice %}}
5. Click on **Next** to continue.
6. You will now scope your job. Create your job with the following parameters or scope.
- Scheduled Job: Selected
- Update Frequency: Daily
- Include existing objects: Selected  
- Sampling Depth: 100%  
- Leave all other settings as default 
7. Click on **Next** to continue.
{{% notice note %}}
We will not be including any custom data identifiers in this job.
{{% /notice %}}
8. Click on **Next** to continue.
9. Give the job a name and description.  

Name|Description
------|-----
**Macie Workshop Scan all buckets**|**Scan all our S3 buckets to discover data using only AWS managed data identifiers**    

10. Click on **Next** to continue.
11. Verify all the details of the job you have created and click on **Submit** to continue.
12. You will see a green banner telling you the ***Job was created successfully***.