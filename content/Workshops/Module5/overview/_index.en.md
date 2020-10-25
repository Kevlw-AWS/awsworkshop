+++
title = "Overview"
menuTitle = "Overview"
date = 2020-07-30T11:04:54-05:00
weight = 5
pre = "<b>1. </b>"
+++

{{% notice note %}}
This workshop is available in the follow region:   
**`us-west-2 (Oregon)`**  
{{% /notice %}}

<h1>Summary</h1>
<p> Your company Chief Information Security Officer (CISO) called you for a special meeting and shared his concerns over the recent audit findings on the customer database where they found a few inconsistencies in the customer’s shipping address and payment
  information. Further investigation reveals unauthorized database activity. The CISO is not comfortable with the password management process of this application and is very suspicious of an insider job for the unauthorized database activity.
  You are tasked to implement a better process to configure application connectivity to the database while eliminating human intervention.</p>
<h3>Rules of the Road</h3>
<p> Use AWS Secrets Manager to remove the hard-coding of database credentials from the API implementations. </p>
<h3>Inventory</h3>
<ul><li>
    <p>Serverless web application</p>
  </li><li>
    <p>RDS Database</p>
  </li><li>
    <p>Lambda functions with RESTful APIs</p>
  </li></ul>
<h3>Getting Started</h3>
<p>Check the Output Properties tab in the Jam and try accessing the URL of the API. This will output the query results run by the Lambda function against the MySQL database. Find the Lambda with hard-coded database credentials and fix them using AWS Secrets Manager.
  Try the API URL again after the fix to make sure query results returned correctly. You will get the answer in a new S3 bucket after you removed the hard-coded password from the Lambda environment variables and have started managing the database password
  correctly. </p>

{{% notice info %}}
Please note, this challenge does require python skills
{{% /notice %}}