# Create a GP3 Volume

First things first, what is a GP3 Volume? I googled and Gemini answered:

"An Amazon EBS gp3 volume is the latest generation of general-purpose solid-state drive (SSD) block storage provided by Amazon Elastic Block Store. It lets you scale storage performance (IOPS and throughput) independently of your storage capacity, while costing up to 20% less per GB than older gp2 volumes."

EBS (Elastic Block Store) provides scalable, high-performance block storage resources for use with Amazon Elastic Compute Cloud (Amazon EC2) instances. https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html

Today, I'll create this through the AWS CLI.

https://docs.aws.amazon.com/ebs/latest/userguide/ebs-creating-volume.html

```
aws ec2 create-volume --volume-type gp3 --size 2 --availability-zone us-east-1
```

After sending, I got the error: An error occurred (InvalidZone.NotFound) when calling the CreateVolume operation: The zone 'us-east-1' does not exist.

So why didn't it create? I removed the 'a' from us-east-1a. It's needed. I looked up why and received the answer below:

"The difference between us-east-1 and us-east-1a is the scope of the infrastructure: us-east-1 is an entire AWS Region, while us-east-1a is a single Availability Zone (AZ) inside that region." 

After rerunning the command, it was created successfully. I still have to name the block store. It has to be named by creating a tag.

```
{
    "AvailabilityZoneId": "use1-az4",
    "Iops": 3000,
    "Tags": [],
    "VolumeType": "gp3",
    "MultiAttachEnabled": false,
    "Throughput": 125,
    "VolumeId": "vol-07668bfc44f8a6a3b",
    "Size": 2,
    "SnapshotId": "",
    "AvailabilityZone": "us-east-1a",
    "State": "creating",
    "CreateTime": "2026-11-16T16:58:55.000Z",
    "Encrypted": false
}
```
### Naming the EBS volume

This will name the EBS volume using tags.

https://stackoverflow.com/questions/12797622/how-to-name-an-ec2-ebs-volume-in-aws-console

```
aws ec2 create-tags --resources vol-07668bfc44f8a6a3b --tags Key=Name,Value="xfusion-volume"
```

### Verifying the volume

```
aws ec2 describe-volumes --volume-ids vol-07668bfc44f8a6a3b --query "Volumes[*].{ID:VolumeId,Tags:Tags}"
```

#### Response to verification

```
[
    {
        "ID": "vol-07668bfc44f8a6a3b",
        "Tags": [
            {
                "Key": "Name",
                "Value": "xfusion-volume"
            }
        ]
    }
]
```

SUCCESS!

### My Thoughts

I would rate this lab as EASY. I did have to look up how to enter the size to ensure it was correct; however, there were no issues when creating this EBS volume. 
