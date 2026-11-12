# Create a Subnet

What is a Subnet?

The thing all us techies struggle with when learning networking. Just kidding. A subnet is a block of small networks created from a larger network. 

Subnetting is the process of dividing a large IP network into smaller logical networks called subnets. Each subnet allows devices to communicate efficiently, improving network performance, security, and manageability. From [Geeksforgeeks](https://www.geeksforgeeks.org/computer-networks/introduction-to-subnetting/).

### Links used:

- https://docs.aws.amazon.com/vpc/latest/userguide/create-subnets.html
- https://docs.aws.amazon.com/cli/latest/reference/ec2/create-subnet.html


# What did I do?

I used the AWS CLI to complete this lab, with the console as a reference.

My first question was, "Do I need a CIDR block to create a subnet in the AWS CLI?" The answer was yes, but the docs aren't too specific about letting you know that it was required.

CIDR block is short for <i>Classless Inter-Domain Routing</i>. It is an IP address allocation method that improves the efficiency of data routing on the Internet. [What is CIDR?](https://aws.amazon.com/what-is/cidr/)

```
aws ec2 create-subnet --vpc-id vpcidhere --cidr-block iprange --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=namhehere}]'
```

BUT I got an error: An error occurred (InvalidSubnet.Conflict) when calling the CreateSubnet operation: The CIDR '172.31.0.0/16' conflicts with another subnet.

To the Google I went!

Gemini let me know that the error meant that I was attempting to "create a subnet with a CIDR block (172.31.0.0/16) that overlaps or duplicates an existing subnet or the entire address space inside your VPC." The fix? See what other IPs are available within the subnet range.

I went to the console and decided to just hit the next IP address after one of the existing ones. I chose 172.31.17.0/20.

THEN BOOM, my networking education kicked in. What am I missing? 

I found an article about the lab that recommended using a [CIDR block checker](https://cidr.xyz/) to see which ranges were available. After checking I decided to go with 172.31.100.0/20. I also decided to change the subnet mask to /24 for a smaller group of IPs.

SUCCESS!

#### new script

```
aws ec2 create-subnet --vpc-id  vpc-id --cidr-block 172.31.100.0/24 --tag-specifications 'ResourceType=subnet,Tags=[{Key=Name,Value=datacenter-subnet}]'
```

```
{
  "Subnet": {
    "SubnetId": "subnet-xxxxxxxx",
    "VpcId": "vpc-xxxxxxxx",
    "CidrBlock": "172.31.100.0/24",
    "AvailabilityZone": "us-east-1f",
    "State": "available",
    "AvailableIpAddressCount": 251,
    "MapPublicIpOnLaunch": false,
    "DefaultForAz": false
  }
}
```

The subnet was created. Overall, this was <b>EASY</b>. I did run into a few bumps when it came to choosing a subnet range that worked. Thanks to the CIDR checker, I was able to pinpoint one and complete the lab.

