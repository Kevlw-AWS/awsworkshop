+++
title = "Review"
menuTitle = "Review"
date = 2020-07-30T11:30:52-05:00
weight = 8
pre = "<b>2. </b>"
+++

## Review S3 batch job details
1. Click on the completed job and ensure it is 100% successful

{{% notice note %}}
You'll notice that in the **Status** section, the `Total succeeded(rate)` is *`5 (100%)`*. Why is that?
{{% /notice %}}

The reason it is 5 is because the total objects that were listed in the manifest to ENCRYPT in the bucket, as part of the batch job were 5.

## Verify our job results in the S3 bucket 
Lets go to our `spoiler` bucket and verify this.

1. Go to [S3 console](https://s3.console.aws.amazon.com/s3/home?region=us-east-2#) and search for your `awsome-film-spoilers-...` bucket.
2. Click on the folder that starts with `job-xyz-...`
3. Click on **results** folder
4. You'll notice a `.csv` file here.
   ![CSV](/images/03-results-excel.png "CSV Output File") 
5.  Open this CSV file. 
6.  The output will show the exact same 5 files have been **Successful** in their encryption. These same files were listed in the `BucketInventory.csv` manifest file.
   ![ExcelCSV](/images/03-excel-manifest.png "Successful matching manifest") 


## Verify one of the 5 files has been encrypted.

1. Click on one of the 5 files listed in the manifest. Let's take `Job Zero.txt` as an example
2. Click on **Properties** and you'll notice that Encryption type is set to `AWS-KMS`
   ![Properties](/images/03-job-zero-properties.png "Job Zero file properties") 
3. Go back to the **Overview** tab and you'll notice the `Server-side encryption` is set to `AWS-KMS` 
   ![Overview](/images/03-job-zero-overview.png "Job Zero Overview") 
4. You'll also observe the KMS key id matches the CMK that Clinton created (and didn't give you access to)

{{% notice info %}}
We can see the power of both S3 batch used in conjunction with KMS's to encrypt bucket contents **WITHOUT** the need for the **OPERATOR** to be given access to the KMS CMK by the **CREATOR** of the key.
{{% /notice %}}