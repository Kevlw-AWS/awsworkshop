+++
title = "Setup Secrets Manager"
date = 2020-07-30T15:08:36-05:00
weight = 10
pre = "<b></b>"
+++

We are going to configure **AWS Secrets Manager** to store and configure rotation and learn how to:
- Store the database credential for the super user of an MySQL database hosted on Amazon RDS
- Store the MySQL database credential used by an application
- Configure Secrets Manager to rotate both MySQL credentials automatically on a schedule that you define

## Store a new Secret in AWS Secrets Manager
1. Navigate to the [AWS Secrets Manager](https://us-west-2.console.aws.amazon.com/secretsmanager/home?region=us-west-2#/home) console.
2. Select **Store a new Secret** (*on the right side*)

{{% notice note %}}
Ignore any banner error messages that may indicate you have no access to Redshift clusters.  This is due to limited permissions in the lab.
{{% /notice %}}

## Setup Credentials for RDS database
3. Select the **Credentials for RDS database** option 
4. Enter the MySQL admin User name and Password 

{{% notice tip %}}
We sourced these credentials in the previous setup from the environment variables in the Lambda function  
**User name**: admin  
**Password**: Test123!
{{% /notice %}}

5. Leave the Encryption Key as the default option (**DefaultEncryptionKey**)
6. Select the MySQL database instance from the list  
   
![Secrets Manager Secret Type](/images/05-secretsmanager-secretType.png)

7. Select **Next** button  

## Store a new secret
8. Give your new secret a name and description.  
  
Field Name| Suggested Value
-----|-----
 **Secret Name**|Applications/MyApp/MySQL-RDS-Database
 **Description**|Superuser for the MySQL database (hosted in RDS) in AWS Sydney Region for the application used in development

![Secrets Manager Sore Secret](/images/05-secretmanager-store_a_new_secret.png)
   
9. Select **Next** button

## Review configuration
10. Keep the defaults for password rotation and click **Next**

{{% notice tip %}}
Take a look at the sample Python code for using Secrets Manager.  Copy this code if you want as we'll be using it to leverage Secrets Manager to connect to our RDS instance.
{{% /notice %}}

```python
# Use this code snippet in your app.
# If you need more information about configurations or implementing the sample code, visit the AWS docs:   
# https://aws.amazon.com/developers/getting-started/python/

import boto3
import base64
from botocore.exceptions import ClientError


def get_secret():

    secret_name = "Applications/MyApp/MySQL-RDS-Database"
    region_name = "us-west-2"

    # Create a Secrets Manager client
    session = boto3.session.Session()
    client = session.client(
        service_name='secretsmanager',
        region_name=region_name
    )

    # In this sample we only handle the specific exceptions for the 'GetSecretValue' API.
    # See https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_GetSecretValue.html
    # We rethrow the exception by default.

    try:
        get_secret_value_response = client.get_secret_value(
            SecretId=secret_name
        )
    except ClientError as e:
        if e.response['Error']['Code'] == 'DecryptionFailureException':
            # Secrets Manager can't decrypt the protected secret text using the provided KMS key.
            # Deal with the exception here, and/or rethrow at your discretion.
            raise e
        elif e.response['Error']['Code'] == 'InternalServiceErrorException':
            # An error occurred on the server side.
            # Deal with the exception here, and/or rethrow at your discretion.
            raise e
        elif e.response['Error']['Code'] == 'InvalidParameterException':
            # You provided an invalid value for a parameter.
            # Deal with the exception here, and/or rethrow at your discretion.
            raise e
        elif e.response['Error']['Code'] == 'InvalidRequestException':
            # You provided a parameter value that is not valid for the current state of the resource.
            # Deal with the exception here, and/or rethrow at your discretion.
            raise e
        elif e.response['Error']['Code'] == 'ResourceNotFoundException':
            # We can't find the resource that you asked for.
            # Deal with the exception here, and/or rethrow at your discretion.
            raise e
    else:
        # Decrypts secret using the associated KMS CMK.
        # Depending on whether the secret is a string or binary, one of these fields will be populated.
        if 'SecretString' in get_secret_value_response:
            secret = get_secret_value_response['SecretString']
        else:
            decoded_binary_secret = base64.b64decode(get_secret_value_response['SecretBinary'])
            
    # Your code goes here. 

```

17. Select the **Store** button

AWS Secrets Manager now has a secret that we'll leverage to connect to our RDS instance.  Let's head over to our Lambda function and make the changes we need.

[Modify Lambda](usesecrets.html) to utilise AWS Secrets Manager.