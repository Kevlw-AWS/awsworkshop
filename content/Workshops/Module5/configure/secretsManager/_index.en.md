+++
title = "Setup Secrets Manager for RDS"
date = 2020-07-30T15:08:36-05:00
weight = 10
pre = "<b></b>"
+++

We are going to configure **AWS Secrets Manager** to store and configure rotation and learn how to:
- Store the database credential for the super user of an MySQL database hosted on Amazon RDS
- Store the MySQL database credential used by an application
- Configure Secrets Manager to rotate both MySQL credentials automatically on a schedule that you define

## Store a new Secret in AWS Secrets Manager
1. Navigate to the [AWS Secrets Manager](https://console.aws.amazon.com/secretsmanager/home) console.
2. Select **Store a new Secret** (*on the right side*)

## Setup Credentials for RDS database
3. Select the **Credentials for RDS database** option 
4. Enter the MySQL admin User name and Password 

{{% notice note %}}
We sourced these credentials in the previous setup from the environment variables in the Lambda function  
-- **User name**: admin  
-- **Password**: Test123!
{{% /notice %}}

5. Leave the Encryption Key as the default option (**DefaultEncryptionKey**)
6. Select the MySQL database instance from the list  
- Your screen should look similar to the image below when you are done.
![Secrets Manager Secret Type](/images/05-secretsmanager-secretType.png)

7. Select **Next** button  

## Store a new secret
8. Give your new secret a name and description.  
  
Field Name| Suggested Value
-----|-----
 **Secret Name**|Database/Development/MySQL-Superuser
 **Description**|Superuser for the MySQL database (hosted in RDS) in AWS Sydney Region for the application used in development

- Your screen should look similar to the image below when you are done.
   
9. Select **Next** button

## Configure Password rotation
10. Select the **Enable automatic rotation** option
11. Change the rotation interval to **60 days**
12. Select the **Create a new Lambda function to perform rotation** option
13. Enter a lambda function name. Example: mysql-rotation-lambda 
14. Select the **Use this secret** option  
- Your screen should look similar to the image below when you are done.
![Secrets Manager New Secret](/images/05-secretsmanager-configureRotation.png)
15. Select **Next** button  

## Review configuration
16. Review **Sample Code**, **Python3** example
*We will reference this code at a later stage
17. Select the **Store** button
18. AWS Secrets manager is now 
- Storing the new secret
- Rotating the RDS password

***This should complete in a couple of minutes***
