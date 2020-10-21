+++
title = "Lab 3: Encrypt the Spoilers"
date = 2019-11-18T08:23:04+11:00
weight = 30
chapter = false
+++

This workshop is designed to help you get familiar with AWS Storage and Security services  and learn how to use them to secure information on cloud. You will be working with S3 Batch operations and Encryption services with KMS. By completing this challenge, you will learn:
* how to create a Batch job to operate on an S3 bucket. 
* Understand how an IAM role with appropriate KMS permissions can help you do encyrpt/decrypt operations.
* How this IAM role can be used to encrypt contents of an S3 bucket using S3 Batch. 

### Lab Overview

{{< rawhtml >}}
<video width="696" height="392" controls>
  <source src="https://apj-security-workshop.s3-ap-southeast-2.amazonaws.com/q4/lab3-intro-ac3.mp4" type="video/mp4">
  Your browser doesn't support video.
</video>
{{< /rawhtml >}}

>  **Speakers: TBD** 

>  *In this video, you’ll also hear from our partner [TBD](https://aws.amazon.com)  highlighting a real-world example of the deployment of the AWS services you’ll use in this lab. For more information, please visit [here](https://aws.amazon.com)*



### Lab Steps
{{% children depth=1 %}}

Click [here](./module3/setup.html) to get started!






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
