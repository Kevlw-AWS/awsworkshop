+++
title = "Configure"
menuTitle = "Configure"
date = 2020-07-30T11:30:52-05:00
weight = 8
pre = "<b>2. </b>"
+++

## Configure S3 Batch Operation
1. Navigate to the S3 Console
2. Click "Batch Operations" on the left menu
3. Create a batch by clicking the orange "Create Job" button on the right
   ![BatchJob](/images/03-create-batch-job.png "Create Batch Job")
4. Ensure the region is "Asia Pacific (Sydney) ap-southeast-2"
5. Select the "Manifest" format to be CSV 
6. Provide the path to the Bucketinventory.csv file in the spoilers bucket by clicking on "Browse S3" button
  ![BucketInventory](/images/03-S3-bucket-inventory.png "Select the manifest")
7. Click "Next"
  ![RegionandManifest](/images/03-final-s3-batch.png "Region and manifest")

## Choose operational parameters

8. Choose the operation type as "Copy"
9.  For the copy destination put the same spoiler bucket by clicking on "Browse S3". .(Select the overwrite checkbox warning - Click on “I acknowledge that existing objects with the same name will be overwritten”)
    ![CopyOperation](/images/03-copy-operation.png "Copy Operation")
10. Leave the Storage class as "Standard"
11. "Enable" Service-side encryption and select Encryption key type as AWS Key Management Service (SSE-KMS). These steps ensure the bucket is encrypted
12. Select the only key which you have access to by selecting "Choose from your KMS master keys"
    ![EnableEncryption](/images/03-enable-encryption.png "Enable Encryption")
13. Leave the remaining parameters unchanged.
14. Select "Next" at the bottom of the form 

## Configure additional options

15. For "Completion Report", again select the spoiler bucket for the "Path to completion report destination" by "Browse S3" and selecting your bucket. 
16. In "Permissions", Choose from existing IAM roles by selecting "S3BatchOperationsRole". This is the role that would give the S3 Batch job ability to encrypt the bucket and all the files given in the manifest.
    ![Permissions](/images/03-permissions-s3-batch.png "Batch Permissions")
17. Click Next

## Review and Create Job

18. Review all the parameters
19. Scroll to the bottom of the page and click the orange “Create job” button

## Now run the newly created job

20. Refresh your screen
21. Confirm the status of your newly created job changes to "Awaiting your confirmation to run".
    ![Awaiting](/images/03-awaiting.png "Awaiting Run")
22. Select the newly created job
23. Click the “Run job” button
24. Scroll to the bottom of the page and click the orange “Run job” button again after verifying job details.
