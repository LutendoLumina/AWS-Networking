<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** Lutendo Matshidze  
**Email:** lupreshie@gmail.com

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service that allows us to create our own isolated networks within an AWS region and control network traffic and security etc..

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to launch a VPC with a public subnet and EC2 instance, and directly accessed/managed an Amazon S3 bucket through the EC2 instance using AWS CLI.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was that Access Keys are required for EC2 instances/ other applications to get access to my AWS enviroment.

### This project took me...

This project took me 90 minutes including demo time.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I will launch a VPC with a public subnet. I also launch an EC2 instance inside that subnet because I need a machine inside my VPC that I can actually connect to and use to test whether my VPC can reach S3. The EC2 instance acts like my “tester computer” inside the network. By placing it in a public subnet, I can easily connect to it (through EC2 Connect or SSH) and then try accessing S3 from inside my VPC to confirm that my setup works.

### Step 2 - Connect to my EC2 instance

In this step, I will directly access an EC2 instance using an EC2 Instance Connect.

### Step 3 - Set up access keys

In this step, I will create access keys so that my EC2 instance can have access to my AWS enviroment, specifically the ability to interact with an S3 bucket.

---

## Architecture set up

I started my project by launching a VPC with a public subnet, and an EC2 instance inside the public subnet.

I also set up an S3 bucket with two files inside.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

AWS CLI is a software we can download into a local computer's terminal so that we can have access to our AWS account and different actiosn without needing to use AWS console. I have access to AWS CLI because its pre-installed in EC2.

The first command I ran was `aws s3 ls`. This command is used to list all S3 buckets inside the AWS account. It is the S3 buckets that the EC2 instance/applicationn has access to.

The second command I ran was `aws configure`. This command is used to set up my EC2 instances credentials in order to access my AWS enviroment.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured an Access key id, Secret access key, default region and default output format.

Access keys are credentials that my EC instance plus other applications needs in order to get access to my AWS enviroment i.e interact with my AWS  resources or services.

Secret access keys are like paswords for my access keys/credentials. My EC2 instance/ other application would need secret access keys as authentication and "log in" to my AWS enviroment.

### Best practice

Although I'm using access keys in this project, a best practice alternative is to use IAM roles with permissions attached. This is a more secure way to grant access to an EC2 instance because it is much easier to track, attach and detach IAM policies.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I will launch an Amazon S3 bucket with two files inside. This S3 bucket will be accessed by my EC2 instance later in the project, so I can test whether my access key has succesfully given AWS access to my EC2 instance.

### Step 5 - Connecting to my S3 bucket

In this step, I will be using AWS CLI commands to try control/manage my S3 bucket. This means I'm interacting with my S3 bucket through my EC2 instance/VPC instead pf the AWS Management Console.

---

## Connecting to my S3 bucket

The first command I ran was `aws s3 ls`. This command is used to list all S3 buckets inside the AWS account. It is the S3 buckets that the EC2 instance/applicationn has access to.

When I ran the command `aws s3 ls` again, the terminal responded with a list of my S3 buckets. This indicated that my Access Keys works i.e my EC2 instanc has access to my AWS enviroment.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was `aws s3 ls s3://nextwork-vpc-project-lutendo` which returned the list of objects inside my S3 bucket.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command `sudo touch /tmp/test.txt` This command creates a blank file called test.txt in my EC2 instance's local directory.

The second command I ran was `aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-lutendo`. This command will copy i.e upload the blank file created into my S3 bucket.

The third command I ran was `aws s3 ls s3://nextwork-vpc-project-lutendo` which returned a list of all my objects in my S3 bucket - including test.txt. This validated that my EC2 instance through AWS CLI commands can get access to other AWS services like S3. 

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-s3_3e1e79a2)

---

---
