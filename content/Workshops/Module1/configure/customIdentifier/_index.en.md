+++
title = "Create a Custom Identifier"
date = 2020-07-30T15:08:36-05:00
weight = 11
chapter = true
pre = "<b></b>"
+++

We are going to create a data classification job that will look for any files that contain the words 'project' and 'unicorn'.  These would indicate that the file contains sensitive information pertaining to our secret project.  To do this we need to create a custom data identifier.  You can follow along with the instructions or attempt to create the regular expression (regex) yourself.

1. Go to the [Custom data identifier](https://console.aws.amazon.com/macie/home#/settings/custom-identifiers) page in the Amazon Macie console.  You will need to click on the **Create** button to begin the process of creating your custom data identifier.  You can also view any previously created custom data identifiers from this page.

![Create Custom data identifier](/images/custom-id-create-1.png)

2. Give your custom data identifier a name and description.  Your screen should look similar to the image below when you are done.   

Name| Description
-----|-----
 **Project Unicorn**|**Find all the confidential project unicorn data**  

![Give it a name and description](/images/custom-id-create-2.png)

3. Now you will need to create a regular expression (regex) to describe the string you wish to match.  Your regex should be able to match any combination of upper and lower case for the word ***unicorn***.  You can test your regular expression using the **Evaluate panel**, how to do this is show in step 5 below.  The regex solution is shown after step 4.  

{{% notice note %}}
Your regular expression should match Unicorn, UNICORN, unicorn, and UnIcOrN.
{{% /notice %}}

4. You will also need to add some **Keywords** to help identify your data and reduce false positives.  Keywords are triggered first followed by the regular expression you created.  Use the following keyword, keywords are not case sensitive:

````
project
````

<details>
<summary>
{{% notice info %}}
Click to expand for the regular expression solution
{{% /notice %}}
</summary>  

Copy and paste the regex if you need (Tip: (?i) makes the regular expression case insentive)

    (?i)unicorn

![Regex Solution](/images/custom-id-create-3.png)  

</details>


5. Test your regular expression and keywords using the **Evaluate** panel.  Use the expressions below to test your keywords and regular expression together.  

````    
Project Unicorn
PROJECT UNICORN
project UnICoRn
````

![Evaluate Expression](/images/custom-id-create-4.png)

6. Click the **Submit** button when you are done creating and testing your Custom Data Identifier

