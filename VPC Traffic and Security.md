<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Traffic Flow and Security

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-security)

**Author:** Lutendo Matshidze  
**Email:** lupreshie@gmail.com

---

## VPC Traffic Flow and Security

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-security_92b0b0b4)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a virtual private network in the AWS cloud where you can launch and manage your resources in a secure, isolated environment.

It is useful because it gives you full control over your network, including IP ranges, subnets, route tables, security groups, and internet access, allowing you to design your cloud architecture exactly the way your applications need.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to create a secure, isolated network where I could launch and organize my cloud resources. I set up my own IP range, created subnets, attached an Internet Gateway, and configured route tables, security groups, and network ACLs to control traffic. This setup ensured my EC2 instances could communicate safely within the VPC and with the internet while being properly protected.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how many different networking components—like subnets, route tables, Internet Gateways, security groups, and network ACLs—have to work together just to get a single EC2 instance online.

### This project took me...

This project took me approximately 3 hours to complete.

---

## Route tables

Route tables are like the GPS that directs traffic within my VPC to the correct destination.

Routes tables are needed to make a subnet public because a subnet needs to have a route to an internet gateway in order to be considered public. A route table is the only way to establish this connection.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-security_0a07b191)

---

## Route destination and target

Routes are defined by their destination and target, which means:
The destination is the range of IP addresses that traffic in my VPC is trying to reach. Think: “Where do I want to go?”
The target is the path or road the traffic will take to get there. Think: “Which road should I take?”

The route in my route table that directed internet-bound traffic to my internet gateway had a destination of 0.0.0.0/0 and a target of my NextWork IG.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-security_0a07b191)

---

## Security groups

Security groups are like security guards that monitor both inbound and outbound traffic at the resource level i.e every single resource in a subnet/VPC has a security group.

### Inbound vs Outbound rules

Inbound rules are rules that monitor or restrict inbound traffic e.g users visiting a wevb app I'm hosting. I  configured an inbound rule that allows all inbound HTTP traffic.

Outbound rules are the rules that monitor/ restrict outbound traffic e.g my web app requesting data from a public source. By default, my security group's outbound rule will allow outbound traffic.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-security_92b0b0b4)

---

## Network ACLs

Network ACLs are like community watchmen that secures my network at a subnet level.

### Security groups vs. network ACLs

The difference between a security group and a network ACL is that their scope (i.e a security group secures my network at a resource level so every resource in my VPC is associated with a security group while network ACLs secures my network at a sybnet level so every subnet in my VPC is associated with my ACL.)

---

## Default vs Custom Network ACLs

### Similar to security groups, network ACLs use inbound and outbound rules

By default, a network ACL's inbound and outbound rules will set up to allow all incoming (inbound) and outgoing (outbound) traffic.

In contrast, a custom ACL’s inbound and outbound rules are automatically set to deny all incoming and outgoing traffic.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-security_4faeb056)

---

## Tracking VPC Resources

What were the three resources you deployed?
I deployed a VPC, an Internet Gateway, and a Security Group.

I created additional resources in a new region instead of my usual region.

Teams would use multiple regions to increase availability, reduce latency for users in different locations, and ensure disaster recovery in case one region goes down.

EC2 Global View is a tool where you can find all your EC2 instances, VPCs, subnets, security groups, and other resources across every AWS region. I could even narrow down my search by region, resource type, or tags. Without EC2 Global View, you'd have to manually switch between regions in the AWS Console to see all your resources, which takes much more time and effort.

Now that I've learnt about EC2 Global View, I'd use it again to quickly track and manage all my VPC resources and EC2 instances across multiple regions, making it easier to monitor usage, check configurations, and ensure everything is set up correctly.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-security_b03ea6162)

---

---
