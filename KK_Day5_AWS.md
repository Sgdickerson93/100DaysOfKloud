# Create a GP3 Volume

First things first, what is a GP3 Volume? I googled and Gemini answered:

"An Amazon EBS gp3 volume is the latest generation of general-purpose solid-state drive (SSD) block storage provided by Amazon Elastic Block Store. It lets you scale storage performance (IOPS and throughput) independently of your storage capacity, while costing up to 20% less per GB than older gp2 volumes."

EBS (Elastic Block Store) provides scalable, high-performance block storage resources for use with Amazon Elastic Compute Cloud (Amazon EC2) instances. https://docs.aws.amazon.com/ebs/latest/userguide/what-is-ebs.html

Today, I'll create this through the AWS CLI.
