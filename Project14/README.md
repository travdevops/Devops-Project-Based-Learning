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