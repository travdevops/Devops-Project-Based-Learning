# AWS Networking Implementation
### VPC - Subnets - IG - NAT - Routing 

### - UNDERSTANDING AMAZON VIRTUAL PRIVATE CLOUD (VPC)

![VPC](<Screenshot 2023-11-19 at 2.06.03 AM.png>)

![Alt text](<Screenshot 2023-11-17 at 1.38.50 PM.png>)

A Default VPC, which Amazon provides for you in each region (think of a region as a separate city), is like a pre-built house in that city. This house comes with some default settings to help you move in and start living (or start deploying your applications) immediately. But just like a real house, you can change these settings according to your needs.

As we want to learn step by step and observe the components, choose the "VPC only" option, we'll use the "VPC and more" option later. Enter "frst-vpc" as the name tag and "10.0.0.0/16 as the IPv4 CIDR. The "10.0.0.0/16" will be the primary IPv4 block and you can add a secondary IPv4 block e.g., "100.64.0.0/16". The use case of secondary CIDR block could be because you're running out of IPs and need to add additional block, or there's a VPC with overlapping CIDR which you need to peer or connect.

![ fr](<Screenshot 2023-11-17 at 1.43.45 PM.png>)

Leave the tags as default, you can add more tags if you want and click `CREATE VPC`

As soon as the VPC is created, it's assigned with a vpc-id and there's a route table created that serves as the main route table - rtb-0d445a10fa97a46f9 in below example.


![dd](<Screenshot 2023-11-17 at 1.44.42 PM.png>)

Now, you need to add subnets

Creating and configuring subnets
What are Subnets?
Subnets are like smaller segments within a VPC that help you organize and manage your resources. Subnets are like dividing an office building into smaller sections, where each section represents a department. In this analogy, subnets are created to organize and manage the network effectively.

     Subnet name        AZ           CIDR block
     subnet-public1a   eu-north-1a   10.0.11.0/24
     subnet-public2b   eu-north-1b   10.0.12.0/24
     subnet-private1a  eu-north-1a   10.0.1.0/24
     subnet-private2b  eu-north-1b   10.0.2.0/24


Go to VPC > Subnets > Create Subnets and select the VPC that you've created previously - the test-vpc or anything you tagged your VPC


Once done, you should see all the subnets you just created on the console. If you missed any, just create a subnet and select your desired VPC. As of now, you can deploy EC2 instances into the VPC by selecting one of the subnets, but the public subnet doesn't have any Internet access at this stage. When you select a public subnet > route,
you'll see it uses the main route table and only has the local route, no default route for Internet access.

![ss](<Screenshot 2023-11-17 at 4.51.16 PM-1.png>)


![subnets](<Screenshot 2023-11-19 at 2.31.51 AM.png>)


![Alt text](<Screenshot 2023-11-19 at 2.33.07 AM.png>)


![Alt text](<Screenshot 2023-11-17 at 4.55.51 PM.png>)

![Alt text](<Screenshot 2023-11-17 at 4.56.19 PM.png>)

We want the private subnets to be private, we don't want the private subnets to have a default route to the Internet. For that, we'll need to create a separate route table for the public subnets


What is a Routing Table?
A Routing Table is like a map or GPS. It tells the people (data) in your city (VPC) which way to go to reach their destination. For example, if the data wants to go to the internet, the Routing Table will tell it to take the road (Internet Gateway) that you built.
Creating and Configuring Routing Tables
Now that we have our entrance and exit (Internet Gateway), we need to give directions to our resources. This is done through a Routing Table. It's like a map, guiding your resources on how to get in and out of your VPC.
Let's go to the route table menu and create a route table for the public subnets.


![Alt text](<Screenshot 2023-11-17 at 5.06.48 PM.png>)

Edit the route table and add the default IGW

![Alt text](<Screenshot 2023-11-17 at 5.08.04 PM.png>)

- Next, Go to the subnet associations tab and click Edit subnet associations

- Select the Public subnets and click save associations

That's it! Now that the VPC is ready, you can run an EC2 instance in public subnets if they need Internet access or in private subnets if they don't.
Note:
**test-vpc-public-rtb**: A route table with a target to Internet gateway is a public route table. test-vpc-private-rtb: A route table with a target to NAT gateway is a private route table.


NAT Gateway and Private Subnets
Introduction to Private Subnets and NAT Gateway
In your AWS Virtual Private Cloud (VPC), private subnets are secluded areas where you can place resources that should not be directly exposed to the internet. But what if these resources need to access the internet for updates or downloads? This is where the NAT Gateway comes in.
A private subnet in AWS is like a secure room inside your house (VPC) with no windows or doors to the street (internet). Anything you place in this room (like a database) is not directly accessible from the outside world.
Understanding NAT Gateway
A Network Address Translation (NAT) Gateway acts like a secure door that only opens one way. It allows your resources inside the private subnet to access the internet for things like updates and downloads, but it doesn't allow anything from the internet to enter your private subnet.
A Network Address Translation (NAT) allows instances in your private subnet to connect to outside services like Databases but restricts external services to connecting to these instances.
Creating a NAT Gateway and Linking It to a Private Subnet
We'll guide you step-by-step on how to create a NAT Gateway and how to link it to your private subnet. We'll also cover how to configure a route in your routing table to direct outbound internet traffic from your private subnet to the NAT Gateway.
Go to VPC > NAT Gateways and click "Create NAT Gateway"

Create the NAT Gateway named "test-nat" under one of the private subnets which I choose the subnet-private1a as the subnet.


![Alt text](<Screenshot 2023-11-17 at 5.36.31 PM.png>)


Choose route table RTB-Private, select Routes tab, and select Add Route. Under the Target, select the NAT gateway named test-nat"


![Alt text](<Screenshot 2023-11-17 at 5.41.46 PM.png>)

Next, go to the "Subnet associations" tab and click "Edit subnet associations"


![Alt text](<Screenshot 2023-11-17 at 5.44.32 PM.png>)

To conclude, we'll revisit the importance of NAT Gateways in the context of private subnets and summarize the key points of the course. We'll also share some best practices when working with private subnets and NAT Gateways in AWS.
By the end of this course, you'll have a clear understanding of how private subnets and NAT Gateways work in AWS and how you can use them to maintain security while allowing necessary internet access for your resources.

## Security Group and Network ACLs
"title": "Security Group and Network ACLs",
### Understanding the Differences between Security Groups and Network Access Control Lists
Security groups and network access control lists (ACLs) are both important tools for securing your network on the AWS cloud, but they serve different purposes and have different use cases.


### Security Groups ![Alt text](SG.png)


Security groups can be compared to a bouncer at a club who controls the flow of traffic to and from your resources in a cloud computing environment. Imagine you have a club, and you want to ensure that only authorized individuals can enter and exit. In this analogy, the club represents your cloud resources (such as virtual machines or instances), and the bouncer represents the security group.
Just like a bouncer checks the IDs and credentials of people at the club's entrance, a security group examines the IP addresses and ports of incoming and outgoing network traffic. It acts as a virtual firewall that filters traffic based on predefined rules. These rules specify which types of traffic are allowed or denied.
For example, a security group can be configured to allow incoming HTTP traffic (on port 80) to a web server, but block all other types of incoming traffic. Similarly, it can permit outgoing traffic from the web server to external databases on a specific port, while restricting all other outbound connections.
By enforcing these rules, security groups act as a line of defense, helping to protect your resources from unauthorized access and malicious attacks. They ensure that only the traffic that meets the defined criteria is allowed to reach your resources, while blocking or rejecting any unauthorized or potentially harmful traffic.
It's important to note that security groups operate at the instance level, meaning they are associated with specific instances and can control traffic at a granular level. They can be customized and updated as needed to adapt to changing security requirements.
Overall, security groups provide an essential layer of security for your cloud resources by allowing you to define and manage access control policies, much like a bouncer regulates who can enter and exit a club.


### Network Access Control Lists {NACLs} ![Alt text](Nacls.png)

Network ACLs (Access Control Lists) can be likened to a security guard for a building, responsible for controlling inbound and outbound traffic at the subnet level in a cloud computing environment. Imagine you have a building with multiple rooms and entry points, and you want to ensure that only authorized individuals can enter and exit. In this analogy, the building represents your subnet, and the security guard represents the network ACL.

Similar to a security guard who verifies IDs and credentials before allowing entry into the building, a network ACL examines the IP addresses and ports of incoming and outgoing network traffic. It serves as a virtual barrier or perimeter security, defining rules that dictate which types of traffic are permitted or denied.

For instance, a network ACL can be configured to allow incoming SSH (Secure Shell) traffic (on port 22) to a specific subnet, while blocking all other types of incoming traffic. It can also permit outgoing traffic from the subnet to a specific range of IP addresses on a certain port, while disallowing any other outbound connections.

By implementing these rules, network ACLs act as a crucial line of defense, safeguarding your entire subnet from unauthorized access and malicious attacks. They ensure that only traffic meeting the specified criteria is allowed to enter or exit the subnet, while blocking or rejecting any unauthorized or potentially harmful traffic.

It's important to note that network ACLs operate at the subnet level, meaning they control traffic for all instances within a subnet. They provide a broader scope of security compared to security groups, which operate at the instance level. Network ACLs are typically stateless, meaning that inbound and outbound traffic is evaluated separately, and specific rules must be defined for both directions.

In summary, network ACLs function as a virtual security guard for your subnet, regulating inbound and outbound traffic at a broader level. They operate similarly to a security guard who controls access to a building by examining IDs, ensuring that only traffic meeting the defined rules is allowed to pass, and thereby providing protection against unauthorized access and malicious activities for your entire subnet.

### In conclusion

![Alt text](secure.png)


In short, security groups and network ACLs are both important tools for securing your network on the AWS cloud, but they serve different purposes and have different use cases.

Security groups are like a bouncer at a club, controlling inbound and outbound traffic to and from your resources at the individual resource level.

Network ACLs, on the other hand, are like a security guard for a building, controlling inbound and outbound traffic at the subnet level.

## VPC & VPN Connection
"title": "VPC Peering and VPN Connection",
### Introduction to VPC Peering

![Alt text](vpc-peering.png)

VPC Peering is a networking feature that allows you to connect two Virtual Private Clouds (VPCs) within the same cloud provider's network or across different regions.

VPC Peering enables direct communication between VPCs, allowing resources in each VPC to interact with each other as if they were on the same network. It provides a secure and private connection without the need for internet access. VPC Peering is commonly used to establish connectivity between VPCs in scenarios such as multi-tier applications, resource sharing, or data replication.
### Benefits of VPC Peering

• **Simplified Network Architecture:** VPC Peering simplifies network design by enabling direct communication between VPCs, eliminating the need for complex networking configurations.

• **Enhanced Resource Sharing:** With VPC Peering, resources in different VPCs can communicate seamlessly, allowing for efficient sharing of data, services, and applications.

• **Increased Security:** Communication between peered VPCs remains within the cloud provider's network, ensuring a secure and private connection.

• **Low Latency and High Bandwidth:** VPC Peering enables high-performance networking with low latency and high bandwidth, improving application performance.

• **Cost Efficiency:** Utilizing VPC Peering eliminates the need for additional networking components, reducing costs associated with data transfer and network infrastructure.

## Introduction to VPN Connections
**VPN (Virtual Private Network)**: connections establish a secure and encrypted communication channel between your on-premises network and a cloud provider's network, such as a VPC. VPN connections enable secure access to resources in the cloud from remote locations or connect on-premises networks with cloud resources.

### There are two primary types of VPN connections:


1. **Site-to-Site VPN**: Site-to-Site VPN establishes a secure connection between your on-premises network and the cloud provider's network. It allows communication between your on-premises resources and resources in the VPC securely and privately. This type of VPN connection is commonly used in hybrid cloud architectures.

![Alt text](site-site.png)

2. **AWS Client VPN**: AWS Client VPN provides secure remote access to the cloud network for individual users or devices. It enables secure connectivity for remote employees, partners, or contractors to access resources in the VPC securely.

![Alt text](aws-client.png)


### Benefits of VPN Connections

• **Secure Remote Access:** VPN connections enable secure access to resources in the cloud network for remote users or devices, ensuring data privacy and protection.

• **Data Encryption**: VPN connections encrypt the data transmitted between your on-premises network and the cloud network, providing a secure channel for data transfer.

• **Flexibility and Mobility**: VPN connections allow authorized users to securely access cloud resources from any location, promoting flexibility and mobility in accessing critical applications and data.

• **Hybrid Cloud Connectivity:** VPN connections play a vital role in establishing secure and reliable connectivity between your on-premises network and cloud resources, facilitating hybrid cloud architectures and seamless integration.

### Summary
In summary, VPC Peering enables direct communication between VPCs, simplifying network architecture and enhancing resource sharing within the cloud network. 

VPN connections establish secure tunnels between on-premises networks and the cloud, enabling secure remote access and facilitating hybrid cloud connectivity. 

Both VPC Peering and VPN connections contribute to building secure, scalable, and efficient network infrastructures in cloud environments.
