# Create a Security Group

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-security-group.html <br>

### What is a security group?

Security groups act as a firewall for associated instances, controlling both inbound and outbound traffic at the instance level. Security groups can be added to EC2 instance or VPCs. 

For VPCs: A security group controls the traffic that is allowed to reach and leave the resources that it is associated with.

# Script

#### Create security group:

```
aws ec2 create-security-group --group-name nautilus-sg --description "Security group for Nautilus App Servers" --vpc-id <id>
```
#### List Security Groups
```
aws ec2 describe-security-groups
```

#### Applied ingress rules for HTTP:

```
aws ec2 authorize-security-group-ingress --group-id sg-000000 --protocol tcp --port 80 --cidr 0.0.0.0/0
```

#### Applied ingress rules for SSH:

```
aws ec2 authorize-security-group-ingress --group-id sg-000000 --protocol tcp --port 22 --cidr 0.0.0.0/0
```

## Validation
```
{
    "SecurityGroups": [
        {
            "GroupId": "sg-0228c5f7df00627c7",
            "IpPermissionsEgress": [
                {
                    "IpProtocol": "-1",
                    "UserIdGroupPairs": [],
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ],
                    "Ipv6Ranges": [],
                    "PrefixListIds": []
                }
            ],
            "VpcId": "vpc-0fe5677fad0eb5efb",
            "SecurityGroupArn": "arn:aws:ec2:us-east-1:123456789012:security-group/sg-0228c5f7df00627c7",
            "OwnerId": "123456789012",
            "GroupName": "nautilus-sg",
            "Description": "Security group for Nautilus App Servers",
            "IpPermissions": [
                {
                    "IpProtocol": "tcp",
                    "FromPort": 80,
                    "ToPort": 80,
                    "UserIdGroupPairs": [],
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ],
                    "Ipv6Ranges": [],
                    "PrefixListIds": []
                },
                {
                    "IpProtocol": "tcp",
                    "FromPort": 22,
                    "ToPort": 22,
                    "UserIdGroupPairs": [],
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ],
                    "Ipv6Ranges": [],
                    "PrefixListIds": []
                }
            ]
        },
        {
            "GroupId": "sg-07b4e46b30f4325cb",
            "IpPermissionsEgress": [
                {
                    "IpProtocol": "-1",
                    "UserIdGroupPairs": [],
                    "IpRanges": [
                        {
                            "CidrIp": "0.0.0.0/0"
                        }
                    ],
                    "Ipv6Ranges": [],
                    "PrefixListIds": []
                }
            ],
            "VpcId": "vpc-0fe5677fad0eb5efb",
            "SecurityGroupArn": "arn:aws:ec2:us-east-1:123456789012:security-group/sg-07b4e46b30f4325cb",
            "OwnerId": "123456789012",
            "GroupName": "default",
            "Description": "default VPC security group",
            "IpPermissions": [
                {
                    "IpProtocol": "-1",
                    "UserIdGroupPairs": [
                        {
                            "UserId": "123456789012",
                            "GroupId": "sg-07b4e46b30f4325cb"
                        }
                    ],
                    "IpRanges": [],
                    "Ipv6Ranges": [],
                    "PrefixListIds": []
                }
            ]
        }
    ]
}

```

<br>

### My Notes

I attempted to create this group through the command line vs going straight the console. I did run into an error trying to figure out how to properly create the script but i figure it out. I also looked up if the group required a VPC or instance or creation and it did. The lab had VPC already created so i was able to debug and applied the group the VPC. My next step was applied the group rules.

I did get some protocol parameter errors but i had to remind myself of port numbers and that TCP works with HTTP.

I would rate this as <b>MEDIUM</b> but leaning towards easy. I ran into a few issue with making sure the script ran and created succesfully. For example i capitalized VPC in the vpc-id, i had to run another with it lowercase. I had the console pulled to make sure the group created and the rules applied.
