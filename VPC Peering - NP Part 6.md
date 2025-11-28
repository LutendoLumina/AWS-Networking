<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Lutendo Matshidze  
**Email:** lupreshie@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational that lets us create our own networks, control traffic flow and security, and organize our resources into public/private subnets.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to setup a multi-VPC architecture (we set up two VPCs), create a peering connection AND update security group rules to run a successful connectivity test to validate my VPC peering setup.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was to need an public IPv4 address for EC2 Instance Connect to work. Also did'nt expect that Elastic IPs can assign static public IP addresses to resources.

### This project took me...

This project took me 2.5 hours including demo time.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will create two VPCs from scratch using the VPC wizard and the visual VPC resource map to speed up the setup process.
Because using the wizard helps me quickly configure the necessary components—such as subnets, route tables, and gateways—without manually creating each resource one by one.

### Step 2 - Create a Peering Connection

In this step, I will be settign up a VPV Peering Connection, which is a VPC component designed to directly connect two VPCs together.

### Step 3 - Update Route Tables

In this step, I will update the route tables in both VPCs because traffic needs to know how to reach the other VPC through the peering connection. Without adding these routes, the VPCs won’t know where to send each other’s traffic, even though the peering connection exists.

### Step 4 - Launch EC2 Instances

In this step, I will launch an EC2 instance in each VPC because I need actual servers inside the VPCs to test whether my VPC peering connection works. Without EC2 instances in both VPCs, there would be no way to check if the networks can really talk to each other.

---

## Multi-VPC Architecture

I started my project by launching two VPCs - they have unique CIDR blocks and they each have one public subnet.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16 respectively. They have to be unique because once you set up a VPC during connection, route table need unique addresses for correct routing across VPCs.

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances because I am using EC2 instance Connect to directly connect with my EC2 instance later in this project, which handles key pairs creation and management for me.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a secure network link that lets two VPCs communicate privately using their private IP addresses.

VPCs would use peering connections to let two separate VPCs communicate with each other using private IP addresses. This allows them to share resources—like databases, servers, or applications—without going over the public internet. Teams use peering to connect different environments (like dev and prod), improve security, reduce costs, and keep their networks simple and private.

The difference between a Requester and an Accepter in a peering connection is that the Requester is the VPC thaat starts the peering connection and the Acccepter is the VPC that recieves the request and must approve it.
Both VPCs can communicate once the connection is accepted, but the process always starts with a requestwr and requres an accepter.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables need to be updated because traffic between VPCs still need directions from each VPC route table in order to get to the other VPC. The default route table does not have a route using the peering connection yet. This needs to be set up so that resources can be directed to the peering connection when trying to reach the other VPC.

My VPCs' new routes have a destination of the other VPC's CIDR block. The routes' target was the peering connection I've set up.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will be using EC2 Instance Connect to connect directly with my first EC2 instance. I need to do this because I need to use my EC2 instance for connectivity tests (to validate  my VPC peering setup) later in this project.

### Step 6 - Connect to EC2 Instance 1

In this step, I will be reattempting my connection to Instance - NextWork VPC 1, and resolving another error preventing me from using EC2 Instance Connect to directly connect with the instance. 

### Step 7 - Test VPC Peering

In this step, I am going to use the Instance - NextWork VPC 1 to attempt a direct connection with the Insttance - NextWork VPC 2 so that we can validate that our peering connection is set up properly.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to directly connect with Instance - NextWork VPC 1 just by using AWS Management Console.

I was stopped from using EC2 Instance Connect as my instance did not have a public IPv4 address. In order for EC2 Instance Connect to work, the EC2 instance must have a public IPv4 address and be in a public subnet.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static public IPv4 addresses that I can request for my AWS Account, and then delegate to specific resources.

Associating an Elastic IP address resolved the error because it gives my EC2 instance a public IP address, fulfilling all the requirements for Instance connect to work.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command `ping 10.2.xxx.xxx` i.e. the private IPv4 address of the other EC2 Instance in VPC 2.

A successful ping test would validate my VPC peering connection because this ping test would not get any replies from the EC2 instance if the peering connection did not successfully connect my two VPCs. Getting ping replies = peering connection was set up properly.

I had to update my second EC2 instance's security group because it was not letting in ICMP traffic - which is the traffic type of ping mesage. I added a new rule that ICMP traffic coming from any resource in the EC2.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-peering_7a29d352)

---

---
