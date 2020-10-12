+++
title = "Investigate the results from the Project Data discovery job"
date = 2020-07-30T15:56:40-05:00
weight = 15
chapter = true
pre = "<b></b>"
+++

You have learnt how to create filters, both *exclude* and *include* and how to use the finding details panel.  For this job you included a custom data identifier. In this section you will gather some information about the files stored with Project Unicorn data in them as well as look at the rememdiation actions taken by the CloudWatch event and Lambda function you configured in an earlier module.

{{% notice tip %}}
Amazon Macie will produce findings for all managed data identifiers.  To reduce the number of results you create a ***suppression rule***.  After you create a 
suppression rule, Macie will continue to generate findings that meet the criteria. However, Macie archives the findings automatically and stops publishing the findings as Amazon CloudWatch events.
{{% /notice %}}

Create the following to test your understanding of how filters work:
1. Which buckets contain files with Project Unicorn data in them? (Hint: Use the custom identifier id in your filter)

<details>
<summary>
{{% notice info %}}
Click to see the solution to finding files and buckets containing project data
{{% /notice %}}
</summary>  

![Project Unicorn data buckets](/images/macie-cdj-1.png)

</details>

2. **(Optional)** Review the actions of the CloudWatch event and Lambda remediation function

The Lambda remediation function was written to take action when triggered by a CloudWatch event related to any findings which were created by the custom data identifier you created.  The function will move the file to a location with the correct security settings and then delete the file.  It will leave a stub file with the same name as the original but with a message to the user.  The Lambda function will also apply the correct data classification tag to the file and send an email to the address provided in the CloudFormation template in Module 1.  

3. To see the message left for the user in the stub file you can follow these steps

    1. Click on a finding from step 1 above.
    2. Look at the findings information panel, under the **Overview** section.
    3. Find the **Resource**.  This will link to the file identified by the finding. Click on this link.
    4. The details of the file in the S3 bucket will open in a new window.
    5. Click the **Download** link to download the file.
    6. Open the file in your favourite text editor and view the message in the file.

4. If all Project Unicorn data should be Confidential, which files are not correctly tagged?

<details>
<summary>
{{% notice info %}}
Click to see the solution for discovering incorrectly tagged Project Unicorn data
{{% /notice %}}
</summary>  

![Project Unicorn incorrect tags](/images/macie-cdj-2.png)

</details>

5. Create a ***suppression rule*** to surface incorrectly tagged objects and hide all correctly tagged and stored project data

    1. Create your filter to *incude* all the findings of interest.
    2. Click on **Suppress findings** to begin to create a suppression rule.
    3. Give your supression rule a name and description.
    4. Click **Save** to save the rule.
    
![Project Unicorn suppression rule](/images/macie-cdj-3.png)

You are now able to create *include* and *exclude* filters and apply filters to Amazon Macie findings.  You can also create and apply a ***suppression rule*** to filter out results.
