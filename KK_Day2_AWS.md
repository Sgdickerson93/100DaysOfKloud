# Create Security Group

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/creating-security-group.html <br>

### What is a security group?

Security groups act as a firewall for associated instances, controlling both inbound and outbound traffic at the instance level. Security groups can be added to EC2 instance or VPCs. 

For VPCs: A security group controls the traffic that is allowed to reach and leave the resources that it is associated with. 

### My Notes

I attempted to create this group through the command line vs going straight the console. I did run into an error trying to figure out how to properly create the script but i figure it out. I also looked up if the group required a VPC or instance or creation and it did. The lab had VPC already created so i was able to debug and applied the group the VPC. My next step was applied the group rules.

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

<br>
I did get some protocol parameter errors but i had to remind myself of port numbers and that TCP works with HTTP.
