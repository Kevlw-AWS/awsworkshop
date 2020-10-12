+++
title = "Scenario"
date = 2020-07-30T11:43:23-05:00
weight = 6
chapter = true
pre = "<b></b>"
+++

Example Corp. has a data classification policy that requires that all documents, whether stored on premises or in the cloud, are tagged with a data classifier.  Data owners are required to include a field, string or tag in the file that reflects this.  The cloud security engineering team has decided to use S3 bucket tags and object tags to help them manage the objects stored in S3.  Buckets containing confidential documents should be encrypted with a customer managed key, Internal buckets can use a service provider managed key but still need to be encrypted and general public buckets can be left unencrypted.  There is also a policy limiting cross account sharing of S3 buckets.

The compliance team has asked for an audit of S3.  They want to make sure there are no publicly shared buckets, that no buckets have cross account sharing enabled and that the required buckets are encrypted with the correct level of encryption.  They have also asked for verification that that all data is tagged and is stored correctly especially focusing on a new project that is just about to be made public.  The project is called Project Unicorn and data should be tagged as Confidential since the project is not yet public.  
