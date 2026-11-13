#  Enable Versioning for S3 Bucket

Today's lab is being completed through the console.

## What is AWS S3?

[Simple Storage Server](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html) x3. It is an object storage service that offers industry-leading scalability, data availability, security, and performance.

### What is an S3 Bucket? 

Where data is stored to be protected and recovered.

Amazon S3 supports four types of buckets: general purpose buckets, directory buckets, table buckets, and vector buckets. Today's bucket is already created as a General Purpose bucket.

https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#BasicsBucket

### What is S3 Versioning?

S3 versioning is used to preserve, retrieve, and restore every version of every S3 object.

https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#Versions

## The Task

I completed this task by following the [Enabling versioning on buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/manage-versioning-examples.html) AWS Console instructions. The instructions were pretty straightforward. I did not encounter any errors or issues while enabling versioning.

### Validation 

I validated via AWS ClI.

```
aws s3api get-bucket-versioning --bucket my-bucket-name
```
#### SUCCESS!

![](./Images/Screenshot%202026-11-12%20at%2011.05.40 PM.png)

## My Thoughts

EASY. EASY. EASY. I know that this is just the tip of the S3 bucket but this lab was very easy but eye opeing to the layers of S3 versioning. 
