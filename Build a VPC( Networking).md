<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Virtual Private Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-vpc)

**Author:** Lutendo Matshidze  
**Email:** lupreshie@gmail.com

---

## Build a Virtual Private Cloud (VPC)

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-vpc_2facf927)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a virtual private network inside the AWS cloud where you can run your resources (like EC2 instances) in a secure and isolated environment. It works like your own private data center but hosted on AWS.

It is useful because it gives you full control over your network — including IP ranges, subnets, route tables, internet access, and security — so you can design your architecture exactly the way your application needs.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a secure, isolated network environment where I could launch and organize my cloud resources. I set up my own IP range, created a subnet, and connected the VPC to the internet using an Internet Gateway so my instances could communicate externally.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how many individual networking components (like a VPC, subnet, and internet gateway) have to work together just to get a simple EC2 instance online.

### This project took me...

This project took me approximately 2 hours including demo time.

---

## Virtual Private Clouds (VPCs)

VPCs are isolated sections of the AWS Cloud that help to keep my AWS resources private and secure.

There was already a default VPC in my account ever since my AWS account was created. This is because AWS has set up a default VPC to allow me to deploy resources like EC2 instances or RDS databases right away (without having to create my own VPC from scratch).

To set up my VPC, I had to define an IPv4 CIDR block, which is a range of IP addresses that my VPC can allocate to the resources deployed into my VPC.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-vpc_2facf927)

---

## Subnets

Subnets are subsections of my VPC, just like how neighbourhoods are subsections of the city. There are already subnets existing in my account, one for every Availability Zone in the region that I set up my VPC in. Since my region is Cape Town (af-south-1), which has 3 Availabilty Zones, I have 3 default subnets already.

Once I created my subnet, I enabled auto-assign public IPv$ addresses. This setting makes sure. that any EC2 instance launched in this subnet automatically gets a public IP, so that can be accessed from the internet and can communicate with the outside world.

The difference between public and private subnets is that public subnets are connected to the internet through an internet gateway which means resources inside a public subnet can communicate with external networks. In contrast, a private subnet does not have direct internet access and is used for internal resources that don't need to be publicly accessible.
 For a subnet to be considered public, it has to have a route to an Internet Gateway.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-vpc_157c4219)

---

## Internet gateways

Internet gateways are the key VPC components that allows internet access for the resources in my VPC/subnet. An internet gateway is also how users in the public can access my resources in apublic subnet.

Attaching an internet gateway to a VPC means resources in your VPC can now access the internet. The EC2 instances with public IP addresses also become accessible to users, so your applications hosted on those servers become public too. 
If I missed this step the VPC would remain isolated, and even EC2 instances with public IPs would not be able to access the internet or be accessed by users. This means any web applications or services hosted on those instances would remain private and unreachable from the outside world.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-vpc_4ae90410)

---

## Using the AWS CLI

VPC resources could also be created with CloudShell, which is shell in your AWS Management Console that lets you run AWS CLI commands without installing anything on your computer. The awesome thing about AWS CloudShell is that it already has AWS CLI pre-installed.
 AWS CLI is a tool that lets you create, delete and update AWS resources with commands instead of clicking through your console.

To create a VPC or subnet using the CLI or CloudShell, you must always include a CIDR block.
This ensures AWS knows the IP address range to assign.

If you don’t include a CIDR block, AWS cannot map IP addresses.

Compared to using the AWS Console, an advantage of using AWS CLI commands is that commands allow you to create resources faster and more consistently, especially when you are repeating tasks. They also make the automation easier and reduce the chance of clicking the wrong option. 

An advantage of using the Console is it provides a visual interface, making it easier to understand the architecture, explore settings, and confirm that resources were created correctly- especially  when you are still learning.

Overall, I preferred using the Console because it feels more intuitive and easier to follow visually, but the CLI is powerful when you want speed, automation, and repeatable setups.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-vpc_9b2465411)

---

---
