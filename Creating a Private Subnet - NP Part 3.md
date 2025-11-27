<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Creating a Private Subnet

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-private)

**Author:** Lutendo Matshidze  
**Email:** lupreshie@gmail.com

---

## Creating a Private Subnet

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-private_afe1fdbd)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is like my own private section of the AWS cloud where I can create and control my networking environment. It lets me build things like subnets, route tables, security groups, and network ACLs in a way that’s isolated and secure.

It is useful because it gives me full control over how my resources communicate — what can enter, what can leave, and what stays private. With a VPC, I can decide which resources should be public, which should be private, how traffic flows, and how everything stays protected. This makes my applications more secure, organized, and reliable.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to build a secure and organized network environment by creating a public subnet, a private subnet, route tables, security groups, and network ACLs. This allowed me to control how my resources communicate, decide what should be publicly accessible, and keep sensitive components safely hidden inside the private subnet.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project is realizing how connected everything in a VPC is — from subnets to route tables to security groups — and how each piece plays a specific role in managing traffic.

### This project took me...

This project took me approximetly 2 hours to complete

---

## Private vs Public Subnets

The difference between public and private subnets is that public subnets are accessible by and can access the internet, while private subnets are completely isolated from the internet by default. 

Having private subnets are useful because keeping resources away from the internet is extremely important for the security of confidential resources.

My private and public subnets cannot have the same IPv4 CIDR block (i.e the same range of IP addresses). The CIDR block for every subnet must be unique and cannot overlap with another subnet.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-private_afe1fdbd)

---

## A dedicated route table

By default, my private subnet is associated with th default route table (i.e the route table that has a route to the internet gateway).

I had to set up a new route table because my subnet can't have a route to an internet gateway.

My private subnet's dedicated route table only has one inbound and one outbound rule that allows internal communication (i.e with the destination of another resource within my VPC).

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-private_b4b904b5)

---

## A new network ACL

By default, my private subnet is associated with the default network ACL that set up with every VPC create in my AWS account.

I set up a dedicated network ACL for my private subnet because a network ACL becomes crucial in an event of security breaches where traffic that has compromised my public subnet can get access to my private subnet if I have network ACL rules that allow all inbound/outbound traffic.

My new network ACL has two simple rules - deny all inbound and deny all outbound traffic.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-private_1ed2cb07)

---

---
