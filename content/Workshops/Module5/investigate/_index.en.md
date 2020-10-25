+++
title = "Investigate"
menuTitle = "Investigate"
date = 2020-07-30T11:04:54-05:00
weight = 6
pre = "<b>2. </b>"
+++

### Lambda

Start by heading over to AWS Lambda and looking at the function that accesses the RDS database.  Can we see any issues with this function?

1. Go to [AWS Lambda](https://us-west-2.console.aws.amazon.com/lambda/home?region=us-west-2#/functions) console
2. Select the `mod-module-1-LambdaRDSTest-[RANDOM]` function
3. See if you can determine how the function gets the password to connect to the database

```python
# rds settings
rds_host = os.environ['RDS_HOST']
name = os.environ['RDS_USERNAME']
password = os.environ['RDS_PASSWORD']
db_name = os.environ['RDS_DB_NAME']
helperFunctionARN = os.environ['HELPER_FUNCTION_ARN']
```

4. And where these values are used to connect to the RDS instance

```python
def openConnection():
    global conn
    try:
        print("Opening Connection")
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

5. There must be a better way to manage these credentials, lets do a bit of reading to come up with a solution

{{% notice tip %}}
[AWS Secrets Manager](https://aws.amazon.com/blogs/security/rotate-amazon-rds-database-credentials-automatically-with-aws-secrets-manager/) might be the perfect solution to having to store credentials in an accessible way, read the linked blog to learn how.
{{% /notice %}}

Head to the [next section](configure.html) to see how we add AWS Secrets Manager to our solution.