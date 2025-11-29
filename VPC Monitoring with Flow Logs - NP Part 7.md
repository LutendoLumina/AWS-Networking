<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Monitoring with Flow Logs

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-monitoring)

**Author:** Lutendo Matshidze  
**Email:** lupreshie@gmail.com

---

## VPC Monitoring with Flow Logs

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_3e1e79a1)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a foundational AWS service that lets us control the underlying network for our resources so that we can control traffic flow, monitor for security, and organize our resources.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to achieve two big milestones! First, I learned to troubleshoot VPC peering connectivity issues. Secondly , I learnt how to monitor network traffic using VPC Flow logs.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was Log Insights have a lot of built-in queries that gives us many maany options on how we'd like to analyze our network's traffic.

### This project took me...

This project took me 2 and half hours to complete(including demo time).

---

## In the first part of my project...

### Step 1 - Set up VPCs

In this step, I will set up two VPCs from scratch in minutes. Network monitoring can still be done with a single VPC but it's great to have the extra challenge to tackle VPC peering in this project too.

### Step 2 - Launch EC2 instances

In this step, I will lauch two EC2 Instances, one in each VPC. Doing this is important to set up the remainder of the project - my EC2 instances will generate the traffic that VPC Flow Logs will monitor.

### Step 3 - Set up Logs

In this step, I will be setting up VPC flow logs to start monitoring network traffic. I am also setting up a storage space for my Flow Logs.

### Step 4 - Set IAM permissions for Logs

In this step, I will provide VPC Flow Logs with the permission to create Logs and upload them into our log geoup in CloudWatch.

---

## Multi-VPC Architecture

I started my project by launching two VPCs. I created two public subnets (i.e one public subnet in each VPC with no private subnet).

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16 respectibly. They have to be unique because having overlaping CIDR block will cause network routing with traffic issues down the line when traffic needs to go from 1 VPC to another.

### I also launched EC2 instances in each subnet

My EC2 instances' security groups allow SSHand ICMP type traffic . This is because EC2 Instance Connect will need to access my EC2 Instace using SSH-type traffic, and because we need to allow ICMP type traffic for connectivity tests later.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_e7fa8775)

---

## Logs

Logs are like diary entries for my computer systems - they are detailed records of any kind of activity related to the traffic/resource/AWS service that the log is tracking.

Log groups are grouping of logs (i.e logs that belong to the project/application/source are often in a log group together!)

### I also set up a flow log for VPC 1

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_e8398869)

---

## IAM Policy and Roles

I created an IAM policy so that I can define a rule that allows policy holders e.g my VPC Flow Logs service the ability to create log streams and upload them into CloudWatch.

I also created an IAM role because services like VPC Flow Logs has to be associated with a role instead of JSOB! Creating an IAM role will be necessary tovgive our VPC Flow Logs the access it needs to record and upload logs.

A custom trust policy is a specific type of policy used for desigining who or what is allowed access to the IAM role.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_4334d777)

---

## In the second part of my project...

### Step 5 - Ping testing and troubleshooting

In this step, I will be generating network traffic. This becomes important when we are communicating about cloudworks/cloud networking/or cloud engineering.

### Step 6 - Set up a peering connection

In this step, I will be setting up a peering connection so that VPCs 1 and 2 can talk directly with each other.

### Step 7 - Analyze flow logs

In this step, I will be tracking the network data that has been collected on my VPCs and then analyze the data to extract insights.

---

## Connectivity troubleshooting

My first ping test between my EC2 instances had no replies, which means ICMP traffic could be blocked by security group or network ACLs, or maybe my traffic is being routed to the wrong path.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_99d4ba42)

I could receive ping replies if I ran the ping test using the other instance's public IP address, which means my second instance isa ctually allowing ICMP and SSH traffic.

---

## Connectivity troubleshooting

Looking at VPC 1's route table, I identified that the ping test with Instance 2's private address failed because I do have a route in my VPC's route tables that directs traffic from one VPC to another

### To solve this, I set up a peering connection between my VPCs

I also updated both VPCs' route tables, so that traffic from one of the VPCs and heading to the other VPC's private IPv4 address can get directed to go through the peering connection instead of the public internet. 

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_7316a13d)

---

## Connectivity troubleshooting

I received ping replies from Instance 2's private IP address! This means setting up the peering connection and then the route table solved the connectivity error of my VPCs traffic not being able to navigate from one VPC to another.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_4ec7821f)

---

## Analyzing flow logs

Flow logs tell us about the source and destination of the network traffic, the amount of data being transferred, whether the traffic was accepted or rejected.

For example, the flow log I've captured tells us that traffic went from the source IP address (10.1.4.242) to the destination address (64.227.182.212).I can also extract that the traffic was accepted by security groups and network ACLs of my VPC.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_d116818e)

---

## Logs Insights

Logs Insights is a special tool within Amazon CloudWatch that helps us with analyzing logs and creating vsual graphs and charts through queries.

I ran the query `Return the top 10 byte transfers by source and destination IP addresses.`. This query analyzes the flow logs collected on EC@ Instance 1, and return the top 10 pairs of IP addresses based on the amount of data transferred between them.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-monitoring_3e1e79a1)

---

---
