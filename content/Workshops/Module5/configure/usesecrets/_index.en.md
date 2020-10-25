+++
title = "Use Secrets Manager programmatically"
menuTitle = "Use Secrets Manager"
date = 2020-09-21T15:08:24-05:00
weight = 20
pre = "<b> </b>"
+++

Now that we have stored the secret in Secrets Manager, we will update our application to retrieve the database credential from Secrets Manager. 

We will use the sample code (as provided by Secrets Manager). This code sets up the client and retrieves and decrypts the secret `Applications/MyApp/MySQL-RDS-Database`.

## Modify Lambda Function
### Function Environment Variables
1. Navigate to the **[AWS Lambda](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions)** console
2. Select the Lambda Function which matches the description in the table below

Function Name| Description
-----|-----
 **mod-module-1-LambdaRDSTest-...**|Test Lambda function to access a RDS Database and read sample data

3. Remove the existing authentication details from the `Environment Variables` section by clicking **Edit** and then **Remove** the two credential variables.

![Secrets Manager Sore Secret](/images/05-secretmanager-ev-before.png)

4. Click **Save** to update the environment variables for this Lambda function

![Secrets Manager Sore Secret](/images/05-secretmanager-ev-after.png)

### Function Code
1. Let's edit the code now starting with our RDS settings.  Find the top section of code and modify it to look like the code below

```python
# rds settings
rds_host = os.environ['RDS_HOST']
db_name = os.environ['RDS_DB_NAME']
helperFunctionARN = os.environ['HELPER_FUNCTION_ARN']

secret_name = "Applications/MyApp/MySQL-RDS-Database"
my_session = boto3.session.Session()
region_name = my_session.region_name
conn = None
```

2. Now replace the `openConnection()` function with the code below

{{% notice info %}}
The code below incorporates the sample code we received when we setup the Secrets Manager secret
{{% /notice %}}

```python
def openConnection():
    print("In Open connection")
    global conn
    name = "None"
    password = "None"
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
        print(get_secret_value_response)
    except ClientError as e:
        print(e)
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
            j = json.loads(secret)
            name = j['username']
            password = j['password']
        else:
            decoded_binary_secret = base64.b64decode(get_secret_value_response['SecretBinary'])
            print("password binary:" + decoded_binary_secret)
            password = decoded_binary_secret.password    

    try:
        if(conn is None):
            conn = pymysql.connect(
                rds_host, user=name, passwd=password, db=db_name, connect_timeout=5)
        elif (not conn.open):
            # print(conn.open)
            conn = pymysql.connect(
                rds_host, user=name, passwd=password, db=db_name, connect_timeout=5)

    except Exception as e:
        print (e)
        print("ERROR: Unexpected error: Could not connect to MySql instance.")
        raise e
```

3. You can now deploy the function and test that your endpoint is still able to query the RDS database.
4. Click on **Deploy** to commit the function