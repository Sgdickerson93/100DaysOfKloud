#  Enable Versioning for S3 Bucket

Today's lab is being completed through the console.

## What is AWS S3?

[Simple Storage Service](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html) x3. It is an object storage service that offers industry-leading scalability, data availability, security, and performance.

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

## 🧠 Cloud Challenge

A client says: "I accidentally deleted an important file from our versioning-enabled S3 bucket. Now I can't find it!" What do you do?

### Steps to take:

1. Open the Amazon S3 Console.
2. Select the affected bucket.
3. Go to the Objects tab.
4. Enable Show versions.
   
This lets you see previous versions of objects, including delete markers.

If the file was deleted normally, S3 places a delete marker on it, making it appear missing even though earlier versions still exist. Removing the delete marker makes the previous version of the S3 object visible again!

<i>One important distinction: Removing a delete marker restores visibility, but permanently deleting a specific object version is a different operation.</i>

