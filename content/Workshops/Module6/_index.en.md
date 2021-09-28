+++
title = "6. Centralise CloudTrail Logs"
date = 2019-11-18T08:23:04+11:00
weight = 32
chapter = false
+++

Logging and monitoring are important parts of a robust security plan. Being able to investigate unexpected changes in your environment or perform analysis to iterate on your security posture relies on having access to data. [AWS recommends that you write logs](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html), especially AWS CloudTrail, to an S3 bucket in an AWS account designated for logging (Log Archive). The permissions on the bucket should prevent deletion of the logs, and they should also be encrypted at rest. Once the logs are centralized, you can integrate with SIEM solutions or use AWS services to analyze them. 

There are 2 options in this lab:

1. If you are using AWS Organizations, you can create a trail that will log all events for all AWS accounts in that organization. You can also choose to edit an existing trail in the management account and apply it to an organization, making it an organization trail. Organization trails log events for the management account and all member accounts in the organization. Please note that if using this option you will need to use an IAM user or role in the management account with [sufficient permissions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/creating-an-organizational-trail-prepare.html#org_trail_permissions).
    
2. If you are not using AWS Organizations, follow this option to create a multi-account Cloudtrail trail. 

### Creating an Organization Trail

1. Please note that if using this option you will need to use an IAM user or role in the management account with [sufficient permissions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/creating-an-organizational-trail-prepare.html#org_trail_permissions).
2. First check that you have enabled all features in your Organization (this should ordinarily be the default when you create an Organization). This is required for you to create an Organization Trail. 
3. From the AWS console, click *Services* and select *AWS Organizations.* 
4. On the left hand side, select *Settings*. 

![Select Settings](/images/Module-6-Image-1.png)

5. Check under Feature Set if your organizations has all features enabled. 

![Feature Set](/images/Module-6-Image-2.png)

6. If if does not, On the [*Settings*](https://console.aws.amazon.com/organizations/v2/home/settings) page choose *Begin process*.
7. On the [*Enable all features*](https://console.aws.amazon.com/organizations/v2/home/settings/enable-all-features) page, acknowledge your understanding that you cannot return to only consolidated billing features after you switch by choosing *Begin process*.
8. AWS Organizations sends a request to every invited (not created) account in the organization asking for approval to enable all features in the organization. If you have any accounts that were created using AWS Organizations and the member account administrator deleted the service-linked role named AWSServiceRoleForOrganizations, AWS Organizations sends that account a request to recreate the role.
9. The console displays the *Request approval status* list for the invited accounts.
10. The [*Enable all features*](https://console.aws.amazon.com/organizations/v2/home/settings/enable-all-features) page shows the current request status for each account in the organization. Accounts that have agreed to the request show a status of *ACCEPTED*. Accounts that haven't yet agreed show a status of *OPEN*.
11. From the AWS console, click *Services* and select *AWS CloudTrail.*
12. Choose *Trails*, and then choose Create *Trail*.

![Create Trail](/images/Module-6-Image-3.png)

13. On the *Create Trail* page, for *Trail name*, type a name for your trail. For more information, see [CloudTrail trail naming requirements](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-trail-naming-requirements.html).

14 Select *Enable for all accounts in my organization*. You only see this option if you are signed in to the console with an IAM user or role in the management account. To successfully create an organization trail, be sure that the user or role has [sufficient permissions](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/creating-an-organizational-trail-prepare.html#org_trail_permissions).

![Enable for all accounts](/images/Module-6-Image-4.png)

15. For *Storage location*, choose *Create new S3 bucket* to create a bucket. When you create a bucket, CloudTrail creates and applies the required bucket policies.
    
16. As best practice, enable SSE-KMS encryption. You can choose to use either a New or Existing KMS key. Click *Next*. 

17. Choose the type of events that you would like CloudTrail to log. [Please note the cost implications of turning on CloudTrail data events.](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-trail-manage-costs.html)You can also choose the API activity, whether you would like to exclude AWS KMS events or exclude Amazon RDS Data API events. 
18. Click *Next*. 

![Click Next](/images/Module-6-Image-5.png)


10. On the next page, select *Create Trail*. Please note that a maximum of 5 Trails can be created in each region. 

Please take a look at this [documentation](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/creating-an-organizational-trail-in-the-console.html) for more information.

### Creating a Multi-Account CloudTrail without AWS Organizations

You can have CloudTrail deliver log files from multiple AWS accounts into a single Amazon S3 bucket for centralisation purposes. 

1. First, you will have to create an S3 bucket for centralisation purposes. 
2. From the AWS console, click *Services* and select *Amazon Simple Storage Service**. *
3. Select *Create Bucket*. 
4. Enter a bucket name. As best practice, select *Block Public Access for this Bucket*. You should also enable server side encryption for this bucket. In this example, you will use SSE-S3, however you can also use a specific SSE-KMS if you would like to encrypt this bucket using AWS KMS. 

![Create a bucket](/images/Module-6-Image-6.png)
![Turn on Block Public Access](/images/Module-6-Image-7.png)
![Turn on Encryption](/images/Module-6-Image-8.png)

5. Click *Create Bucket*. 
6. Next, *find the bucket that you have create and select it*. For a bucket to receive log files from multiple accounts, its bucket policy must grant CloudTrail permission to write log files from all the accounts you specify. This means that you must modify the bucket policy on your destination bucket to grant CloudTrail permission to write log files from each specified account.
7. Choose *Permissions*. 

![Choose Permissions](/images/Module-6-Image-9.png)

8. Choose *Edit Bucket Policy*.
9. Modify the existing policy to add a line for each additional account whose log files you want delivered to this bucket. 

    {
    "Version": "2012-10-17",
    "Statement": [
    {
    "Sid": "AWSCloudTrailAclCheck20131101",
    "Effect": "Allow",
    "Principal": {
    "Service": "cloudtrail.amazonaws.com"
    },
    "Action": "s3:GetBucketAcl",
    "Resource": "arn:aws:s3:::myBucketName"
    },
    {
    "Sid": "AWSCloudTrailWrite20131101",
    "Effect": "Allow",
    "Principal": {
    "Service": "cloudtrail.amazonaws.com"
    },
    "Action": "s3:PutObject",
    "Resource": [
    "arn:aws:s3:::myBucketName/AWSLogs/111111111111/*",
    "arn:aws:s3:::myBucketName/AWSLogs/222222222222/*"
    ],
    "Condition": {
    "StringEquals": {
    "s3:x-amz-acl": "bucket-owner-full-control"
    }
    }
    }
    ]
    }

As an example: 

![Sample bucket policy](/images/Module-6-Image-10.png)
10. Click *Create Bucket Policy*. Your bucket will now receive CloudTrail Log files from all accounts that you specify. You will need to edit this bucket policy for each new trail that you would like to centralise into this bucket. 

You will now have to create CloudTrail trails in each of the accounts that you had granted bucket policy permissions for. Alternatively, if you have a trail that you would like to centralise into this bucket you may also choose to do so. 
1. From the AWS console, click *Services* and select *AWS CloudTrail**. *
2. Click *Create Trail.*
3. Enter a trail name. 
4. For storage location, click *use existing S3 bucket*. Search for the bucket that you have just created to centralise your trail into. As best practice, enable log file creation. 

![Click use existing S3 bucket](/images/Module-6-Image-11.png)

5. Click *Next*. 
6. Choose the type of events that you would like CloudTrail to log. [Please note the cost implications of turning on CloudTrail data events.](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-trail-manage-costs.html) You can also choose the API activity, whether you would like to exclude AWS KMS events or exclude Amazon RDS Data API events. 
3. Click *Next*. 

![Choose the type of events for CloudTrail to log](/images/Module-6-Image-11.png)

8. On the next page, select *Create Trail*. Please note that a maximum of 5 Trails can be created in each region. 
9. You can now create trails in all of the AWS accounts that you would like to centralise into the S3 bucket created above.

For more information please take a look at our [documentation.](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)