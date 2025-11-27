<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Launching VPC Resources

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-ec2)

**Author:** Lutendo Matshidze  
**Email:** lupreshie@gmail.com

---

## Launching VPC Resources

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-ec2_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service that hepls us create our own networks and configure the security/traffic rules and connectivity with the internet.

### How I used Amazon VPC in this project

I used Amazon VPC to create my own VPC with different resources/components (e.g security groups, network ACLs), private resources (e.g private subnet) and EC2 instances in both my public and private subnets.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was the resource map to be so visual and interactive. Such a convenient and speedy way to sert up an entire VPC architecture.

### This project took me...

This project took me approximately 2.5 hours to complete including a live demo time.

---

## Setting Up Direct VM Access

Directly accessing a virtual machine means logging into the EC2 instance (instead of just managing it at a higher level with the AWS Management Console). This includes operations like installing software and changing my EC2 instance configurations.

### SSH is a key method for directly accessing a VM

SSH traffic means Secure Shell, and it is both a protocol and a traffic type. It is the protocol that matches key pairs and enables direct VM access, and once a connection is set up, it is a traffic type that encrypts communication/data being transferred.

### To enable direct access, I set up key pairs

Key pairs are tools that help developers/engineers authenticate themselves when trying to get direct access to a virtual machine e.g an EC2 instance.
Key pairs work by having two private keys - a private key for the VM and a matching private key for the resource/user.

A private key's file format means the file type that my key is stored in. My private key's file format was .pem which is a widely accepted file format that most servers will be able to read/use.

---

## Launching a public server

I had to change my EC2 instance's networking settings by changing the VPC and the subnet my Ec2 instance was going to be launched in! I updated both to my NextWork VPC and my public subnet respectibly. I also used my existing oublic security group.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-ec2_88727bef)

---

## Launching a private server

My private server has its own dedicated security group because the NextWork public security group allows in ALL HTTP traffic - which would leave our private server much more vulnerable to security attacks.

My private server's security group's source is my NextWork Security Group. which means only SSH traffic coming from resources associated with that security group  will be allowed.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-ec2_4a9e8014)

---

## Speeding up VPC creation

I used an alternative way to set up an Amazon VPC! This time, I used the VPc and more option which gives me a resource map to use when creating the VPC and all off its components e.g security groupd, route tables, and internet gateways.

A VPC resource map is a visual diagram that maps out my VPC's components AND the relationship connections between them. A resource map is interactive (i.e it will highlight the connections relevant to a resource that I highlight/hover over).

My new VPC has a CIDR block of 10.0.0.0/16. It is possible for my new VPC to have the same IPv4 CIDR block as my existing NextWork VPC because VPC's are already isolated from each other. Still, this is not the best practice if we need VPC pairing.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-ec2_1cbb1b88)

---

## Speeding up VPC creation

### Tips for using the VPC resource map

When determining the number of public subnets in my VPC, I only had two options: either than none or 1 in each availability zone for my VPC. This was because it is besrt practice (improves redundancy and higher availability to have atleast one subnet per availability zone).

The set up page also offered to create NAT gateways, which are connectors/gateways that will let resources in my private subnet get access to the internet (e.g for security updates) while still blocking off incoming traffic from the internet.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-ec2_8ee57662)

---

---
