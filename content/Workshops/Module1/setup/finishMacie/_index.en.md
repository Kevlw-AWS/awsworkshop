+++
title = "Finish Macie setup"
menuTitle = "Finish Macie setup"
date = 2020-07-30T14:27:45-05:00
weight = 14
chapter = true
pre = "<b></b>"
+++

### Configure Amazon Macie to export findings to an S3 Bucket
Now that the environment is setup you need to complete the setup of Amazon Macie.  When Amazon Macie runs a data discovery job, it creates a discovery result record for each Amazon S3 object that the job analyzes or attempts to analyze. This includes objects that don't contain sensitive data, and therefore don't produce a finding, and objects that Macie isn't able to analyze due to issues such as permissions errors or use of an [unsupported format](https://docs.aws.amazon.com/macie/latest/user/discovery-supported-formats.html). If an object does contain sensitive data, the record indicates where Macie found each occurrence of sensitive data in the object: the line number for text files; the page number for Adobe Portable Document Format (PDF) files; or, the record number for Apache Avro object containers and Apache Parquet files.

To access these records and enable long-term storage and retention of them, you can configure Macie to store the records in an S3 bucket and encrypt them using an AWS Key Management Service (AWS KMS) key. If you do this, Macie starts writing your discovery results to JSON Lines files, which it adds to the S3 bucket as GNU Zip (GZ) files. Consequently, the S3 bucket can serve as a definitive, long-term repository for all of your discovery results. If you don't configure this type of repository for your discovery results, Macie stores the results for 90 days. 

1. Go to the [Amazon Macie](https://console.aws.amazon.com/macie/home) console.
2. Click on [Discovery Results](https://console.aws.amazon.com/macie/home#/settings/repository-for-discovery-results) in the left hand menu.
3. Click on the **Configure Now** option under the section ***Respository for sensitive data discovery results***.

![Repository for sensitive data discovery results](/images/s3-results-repo-1.png)

4. Select the **Existing Bucket** option 
5. Using the dropdown called **Choose Bucket** select the bucket named **macieworkshop-env-setup-resultsbucket-\<randomstring\>**.
6. Under the KMS encryption section select the option **Select a key from your account** 
7. Using the KMS key alias dropdown select the KMS key called **MacieWorkshop-Env-Setup-results-bucket-encryption-key**.
8. Your setup should resemble to image below.

![Respository for discovery results setup](/images/s3-results-repo-2.png)

9. Click Save to continue.  

{{% notice note %}}
You should see a green banner indicating "Success".  If you see a red banner with an error message, please double check that you have selected the correct S3 bucket and KMS key.
{{% /notice %}}

You are now setup for the workshop!