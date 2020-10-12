+++
title = "Create the second Data Classification Job"
date = 2020-07-30T15:09:13-05:00
weight = 16
chapter = true
pre = "<b></b>"
+++

Now you are going to create the second Data Classification job so you can evaluate the contents of your S3 buckets.  This second job you create will run once and evaluate the contents of the Internal and Public tagged buckets looking for project unicorn data.  This job will use a custom data identifier.

1. Go to the [Macie console](https://console.aws.amazon.com/macie/home)
2. To begin, select the **S3 buckets** option in the left hand menu
3. Select the two S3 buckets labeled 
- macieworkshop-env-setup-publicbucket-\<random\>
- macieworkshop-env-setup-internalbucket-\<random\>  
4. Click on the **Create job** button 
{{% notice note %}}
You are now able to verify the S3 buckets you chose before you continue, use the **Previous** or **Remove** buttons if you selected the incorrect S3 buckets.  
{{% /notice %}}

5. Applying the skills you learnt creating the first classification job, create the second job with the following scope parameters:
- One-time job
- Sampling Depth of 100%
- Include Tags with Key of Classification and Value of Internal (Hint: Expand ***Additional Settings*** and use the **Add Tag** button to add multiple tags)
- Include Tags with Key of Classification and Value of Public
- Specify the Custom data classifier created in step 1  

<details>
<summary>
{{% notice info %}}
Click to view the solution to creating the second classification job
{{% /notice %}}
</summary>  

![Solution to Job two](/images/macie-solution-job2.png)

</details>

6. Give the job a name and description  

Name | Description
-----|-----
**Macie Workshop Project Data**|**Scan Public and Internal buckets for secret project data using a custom identifier**  

Well Done! You can now create a custom data indentifier and create different types of data classification jobs!
