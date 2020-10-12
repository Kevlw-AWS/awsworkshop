+++
title = "Investigate the results from the Scan all buckets job"
date = 2020-07-30T15:56:17-05:00
weight = 12
chapter = true
pre = "<b> </b>"
+++

Amazon Macie produces findings.  Interpreting the findings is how you develop an understanding into how your data is stored in your environment.  For this job you configured your scan to use only the included managed data identifiers.  In this section you will use the **Findings** menu option to view and filter the findings that were created by the two jobs you configured in Module 2.  We will investigate some of the filter types and methods for applying them.

1. Return to the [Macie console](https://console.aws.amazon.com/macie/home)
2. Click on the **Jobs** menu item
3. Select the first job you created, it should be called **Macie Workshop Scan all buckets**
4. In the right hand details panel, click on the **Show results** button
5. Click on **Show findings**
6. You are now presented with the findings screen, filtered by Job Id.
7. From here you can add to or remove filters to change the findings you see.

To create your first filter, we are going to include all findings that contain credentials and are tagged with a classification of public.

1. Click on *Add filter*
2. Select the filter type called **Finding type**
3. You are presented with a selection of available finding types.  Select the checkbox for ***SensitiveData:S3Object/Credentials***.
4. Click Apply
5. Click on *Add filter*
6. Scroll down and select the **S3 object tag key** and enter the value of **Classification** *(Filters are case sensitive)*
7. Click **Apply**
8. Click on *Add filter*
9. Scroll down and select the **S3 object tag value** and enter the value of **Public** *(Filters are case sensitive)*
10. Click **Apply**

You should see a list of files, these files contain credentials and are tagged as public.  By clicking one of the findings you will see the details panel on the right side appear.  You can see all the details of the file.  Scroll down and review the details of the file that resulted in the finding.

{{% notice note %}}
What S3 bucket is this file stored in?  
Do you think this file is in the correct S3 bucket?  
Are there files tagged as public stored in the incorrect buckets?
{{% /notice %}}

When you create a filter it can be an *include* filter or *exclude* filter.  The default is an *include* filter.  By clicking on the black circle next to the filter type you can change this.  

Include Filter ![Include filter](/images/macie-filter-include.png)  
Exclude Filter ![Exclude filter](/images/macie-filter-exclude.png)  

Our next filter will show us which files contain US Social Security numbers and if any of them are located in Public buckets.

1. To clear the filters you created use the large X at the end of the filter box, just after "Save rule"

![Clear filter](/images/macie-filter-clear.png)  

2. Click *Add filter*
3. Select the filter type called **Sensitive data detection type** 
4. Enter **USA_SOCIAL_SECURITY_NUMBER** 
5. Click Apply  

![Filter for SSN](/images/macie-filter-ssn.png)

Our example organization uses bucket tags to identify which buckets can be public so lets use that as the next filter criteria.  

6. Click *Add filter*
7. Scroll down and select the **S3 bucket tag key** and enter the value of **Classification** *(Filters are case sensitive)*
8. Click **Apply**
9. Scroll down and select the **S3 bucket tag value** and enter the value of **Confidential** *(Filters are case sensitive)*
10. Click **Apply**
11. Change the filter to an *exclude* filter

![Filter for SSN](/images/macie-filter-ssn-2.png)

{{% notice note %}}
Can you find out which files contain credit card numbers?  
Which buckets are those files stored in?  
Are any of the files encrypted, are any unencrypted?  
{{% /notice %}}

<details>
<summary>
{{% notice info %}}
Click to expand for the solution
{{% /notice %}}
</summary>

Create a filter using the **Sensitive data detection type** and filter on **CREDIT_CARD_NUMBER**  
![Credit Card number solution](/images/macie-filter-cc.png)  

Click on a finding to display the finding details panel.  The bucket name and encryption status can be found in the details panel.  
![Bucket name solution](/images/macie-filter-bucket.png)  

Scroll down to find the object properties  
![Encrypted and not](/images/macie-filter-encrypted.png)

</details>

An additional method to create a filter is to use the right hand details panel.  Next to each of the details in the panel is a magnifying glass with a + that creates an *include* filter and a magnifying glass with a - that creates an *exclude* filter.  

![Include and Exclude filters](/images/macie-filter-inc.png)
