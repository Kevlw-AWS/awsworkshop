+++
title = "Lab 3: Encrypt the Spoilers"
date = 2019-11-18T08:23:04+11:00
weight = 30
chapter = false
+++

This workshop is designed to help you get familiar with AWS Storage and Security services  and learn how to use them to secure information on cloud. You will be working with S3 Batch operations and Encryption services. By completing this challenge, you should learn how to create a Batch job to operate on an S3 bucket. You will also use the Batch Operation to encrypt the file.

Scenario:

The Head of Privacy for AWSome Films, Clinton, has tasked you with encrypting the movie plot spoilers contained in the awsome-film-spoilers bucket (eg. awsome-film-spoilers-140a9c16-7bb1-4d00-a618-b3b178edb3a3). Clinton is so concerned with ensuring that these spoilers are not leaked that he has had a KMS key created for the encryption, but has not granted you access to use it. He said that the S3BatchOperationsRole role has been given permissions to encrypt S3 objects with the KMS key and that you can use that to accomplish the task. Clinton has also asked that the spoilers remain in the same folder with the same names so it won’t cause the Privacy team’s automation to break. Lastly, he mentions all the spoilers to be encrypted are listed in a file named BucketInventory.csv.

Account Inventory:

* awsome-film-spoilers S3 bucket
    * Bucket inventory file included
* Customer Managed KMS Key
* S3BatchOperationsRole IAM role


Architecture:


For this workshop, you will use single s3 bucket in the Sydney, ap-southeast-2 region and IAM role to carry out encryption of bucket file through S3 batch operation.


Region:
Please use the Sydney, ap-southeast-2 region for this workshop.

Modules:


1. Creation of S3 Batch Operation job
2. Begin copy Operation setup
3. Encrypt the file with Batch role
4. Running the job



1: Start creation of an S3 Batch Operation


* Navigate to the S3 console page
* Click "Batch Operations" on the left menu

[Image: image.png]

* Create a batch by clicking the orange "Create Job" button on the right

[Image: image.png]

2: Begin copy operation setup
While creating the job,


* Select the csv option for the manifest
* Provide the path to the BucketInventory.csv file in the spoilers bucket.
* Click next

[Image: image.png]

* Choose the copy operation

[Image: image.png]

* For the copy destination put the spoiler bucket ARN where the objects currently exist.(Select the overwrite checkbox warning - Click on “I acknowledge that existing objects with the same name will be overwritten”)

[Image: image.png]3: Encrypt the files with the Batch role

Fill in the remaining parameters

[Image: image.png]
* Select the box for Server Side Encryption
* Select the SSE-KMS option
* Select the "Choose from your KMS master keys" Option
* Select the only key to which you have access to see

[Image: image.png]
* Leave the remaining parameters unchanged.
* Select next at the bottom of the form


[Image: image.png]

* 
* Select the spoiler bucket ARN for the "Path to completion report destination"
* At the bottom of this page select the S3BatchOperationsRole for the IAM Role

[Image: image.png]
* Click next
* Add any optional tags.
* Review all the parameters
* Scroll to the bottom of the page and click the orange "Create job" button


4. Run the job
[Image: image.png]

* Select the newly created job
* Click the "Run job" button
* Scroll to the bottom of the page and click the orange "Run job" button

[Image: image.png]
Helpful Links
https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html
[https://docs.aws.amazon.com/AmazonS3/latest/user-guide/batch-ops.html](http://a/)
