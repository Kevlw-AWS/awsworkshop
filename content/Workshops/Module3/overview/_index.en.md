+++
title = "Introduction"
date = 2020-07-30T11:04:54-05:00
weight = 5
pre = "<b>0. </b>"
+++

{{% notice note %}}
This workshop is available in the follow region:   
**`us-east-2 (Ohio)`**  
{{% /notice %}}

## Scenario

The Head of Privacy for AWSome Films, Clinton, has tasked you with encrypting the movie plot spoilers contained in the awsome-film-spoilers bucket (eg. awsome-film-spoilers-140a9c16-7bb1-4d00-a618-b3b178edb3a3). Clinton is so concerned with ensuring that these spoilers are not leaked that he has had a KMS key created for the encryption, but has not granted you access to use it. He said that the S3BatchOperationsRole role has been given permissions to encrypt S3 objects with the KMS key and that you can use that to accomplish the task. Clinton has also asked that the spoilers remain in the same folder with the same names so it won’t cause the Privacy team’s automation to break. Lastly, he mentions all the spoilers to be encrypted are listed in a file named BucketInventory.csv.

### Architecture

For this workshop, you will use single s3 bucket in the Sydney, ap-southeast-2 region and IAM role to carry out encryption of bucket file through S3 batch operation. 

![Architecture](/images/03-arch.png "Workload Architecture")

### Modules
This workshop is broken down into four modules

1. Setup
2. Configure S3 Batch
3. Investigate and Understand
4. Review and Discussion