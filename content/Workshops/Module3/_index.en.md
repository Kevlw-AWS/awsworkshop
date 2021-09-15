+++
title = "3. No Hardcoding Secrets"
date = 2019-11-18T08:23:04+11:00
weight = 29
chapter = false
+++

When you build applications on AWS, you can use AWS IAM roles to deliver temporary, short-lived credentials for calling AWS services. However, some applications require longer-lived credentials, such as database passwords or other API keys. If this is the case, you should never hard code these secrets in the application or store them in source code.

You can use AWS Secrets Manager (https://aws.amazon.com/secrets-manager/) to control the information in your application. Secrets Manager allows you to rotate, manage, and retrieve database credentials, API keys, and other secrets through their lifecycle. Users and applications can retrieve secrets with a call to Secrets Manager APIs, eliminating the need to hard code sensitive information in plain text.

Please note that this exercise is *OPTIONAL* and only applicable if you have an existing Amazon Relational Database Service (RDS) MySQL server, Amazon Elastic Container Service (ECS) cluster (with a container-based application), Amazon Elastic Container Registry (ECR). 

### Steps - Replace Hardcoded Credentials (OPTIONAL)

1. From the AWS console, click Services and select Secrets Manager.

2. On the Secrets Manager console click on Store a new secret.

![Click Store a new secret](/images/Module-3-Image-1.png)

3. On ‘Store a new secret’ screen click on Select the *Credentials for RDS database* radio button.

![Click Credentials for RDS database](/images/Module-3-Image-2.png)

4. Enter the values for User name and Password fields respectively.

5. Select *DefaultEncryptionKey* in the dropdown menu.

![Select DefaultEncryptionKey](/images/Module-3-Image-3.png)

6. Scroll down to the bottom of the page and you will see a list of your RDS instances. Select the RDS instance for which you want to store the secret.
    
![Select the RDS instance](/images/Module-3-Image-4.png)

7. Click Next.

8. Enter a name for the secret and provide optional description.

![Enter a name](/images/Module-3-Image-5.png)

9. Click *Next*.

10. On ‘Configure automatic rotation’ screen leave the default values as is i.e., Disable automatic rotation, click *Next*.

11. On the Review screen, click *Store*. You will see a message saying that your secret has been successfully stored.

12. Now click the *Secret name* that you have just created.

13. Copy the *Amazon Resource Name or ARN* for later use.

![Copy the ARN](/images/Module-3-Image-6.png)

14. From the AWS console, click *Services* and select *Elastic Container Service*.

15. Select the Clusters menu item to view the stack that you want to configure.

![Select the Clusters menu Item](/images/Module-3-Image-7.png)

16. Click the *Task Definitions* menu item.

17. Click the check box next to the appropriate task definition name and then click *Create new revision*.
    
![Click create new revision](/images/Module-3-Image-8.png)

18. Leave all of the current values in place. Scroll down and *click Configure via JSON.* 

![Click configure via JSON](/images/Module-3-Image-9.png)

19. Look for the list named secrets. It should have null value for now i.e., ““secrets”:null,”

20. Edit text and insert the copied ARN of the secret that was created earlier i.e., smsdemo, as shown below.  

    "secrets": [
    {
    "valueFrom" :"<paste the ARN you copied earlier">
    "name": :TASKDEF_SECRET"
    }
    ]

![JSON text](/images/Module-3-Image-10.png)

21. Click Save to save the revised JSON definition.

22. Click Create to create the new revision of the Task Definition that includes the JSON revisions.

23. You will see a message saying that the new revision has been created. Notice that the revision has a version number attached to it as shown in the figure below.

![MEssage](/images/Module-3-Image-11.png)

For more information please read the [AWS User Guide](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)

You should also learn how to use [AWS IAM roles for applications running on Amazon EC2](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html). Also, for best results, learn how to [securely provide database credentials to AWS Lambda functions by using AWS Secrets Manager](https://aws.amazon.com/blogs/security/how-to-securely-provide-database-credentials-to-lambda-functions-by-using-aws-secrets-manager/).