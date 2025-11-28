<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Testing VPC Connectivity

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-connectivity)

**Author:** Lutendo Matshidze  
**Email:** lupreshie@gmail.com

---

## Testing VPC Connectivity

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-connectivity_8ee57662)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is AWS's foundational networking service. Having VPCs is th reason why our resources can be made private or public to the internet. We also set up our own network's traffic flow/security rules using a VPC.

### How I used Amazon VPC in this project

In today's project, I used Amazon VPC to set up a VPC's and its components using the BPC wizard, and then launched EC2 instances AND tested the connectivity between my networks resources.

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was to run into an error due to a network ACL's Source pointing to an incorrect subnet CIDR block. This was a great reminder of the importance to slow down and double check configuration settings when using the VPC wizard to automate creating the VPC.

### This project took me...

This project took me approximately 2 hours and 45 minutes including live demo time and triubleshooting an unexpected error.

---

## Connecting to an EC2 Instance

Connectivity means getting resources in our network to communicate with each other and how well they can communicate delivered data to each other. Without connectivity , resources in our network cannot communicate e.g users can't access our application.

My first connectivity test was whether I could connect to my Nextwork's Public Server ( an EC2 instance).

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-connectivity_88727bef)

---

## EC2 Instance Connect

I connected to my EC2 instance using EC2 Instance Connect, which is a tool provided by Amazon EC2 that allows us to directly access an EC2 instance using the AWS Management Console! We no longer need to manager key pairs or use an SSH client to get access.

My first attempt at getting direct access to my public server resulted in an error, because my Private Server had a security group that did not allow SSH traffic, it only allowed HTTP traffic i.e a different protocol.

I fixed this error by addign a new inbound rule in my Private Server's Security Group that allows any SSH traffic from anywhere.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-connectivity_1cbb1b88)

---

## Connectivity Between Servers

Ping is a tool to test the connectivity between two servers and also the response times (i.e the performance of the connection). I used ping to test the connectivity between my Public and Private servers.

The ping command I ran was `ping 10.0.1.84` where 10.0.1.84 is the private IPv4 address of my private server.

The first ping returned NOreplies from the Private Server. This meant security settings with my private server was blocking ICMP inbound (annd or outbound) ICMP traffic, which is the traffic type of ping messages.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-connectivity_defghijk)

---

## Troubleshooting Connectivity

I troubleshooted this by enabling ICMP traffic in my private server's network ACLs and security groups!
As a bonus, I also made sure the Source I defined in my network ACL correctly pointed to my Public Subnet.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-connectivity_4a9e8014)

---

## Connectivity to the Internet

Curl is a connectivity tool that tests connectivity from a server to another server and retrieves data from the target server too.

I used curl to test the connectivity between my network's Public Server with the public internet. This test would only be successful if my internet gateway, network ACLs, security groups and route tables were set up correctly.

### Ping vs Curl

Ping and curl are different because return different responses to my Server's terminal - ping responds with a report on the performance of connectivity with my private server and url responded with html data from another public server.

---

## Connectivity to the Internet

I ran the curl command  `curl https://learn.nextwork.org/projects/aws-host-a-website-on-s3` which returned the html content of nextwork's first project guide.

![Image](http://learn.nextwork.org/charmed_beige_timid_seahorse/uploads/aws-networks-connectivity_8ee57662)

---

---
