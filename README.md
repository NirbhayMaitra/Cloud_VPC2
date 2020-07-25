## Creating a web portal for our company with all the security as much as possible using a Wordpress software with a dedicated database server in which Database is not accessible from the outside world for security purposes. Only the Wordpress is accessible to Clients. An additional feature has been added which is a NAT Gateway to provide the internet access to instances running in the private subnet.
### Before explanation of my task, let me introduce you to these terms.

# Virtual Private Cloud(VPC)

<img src="images/vpc2.jpg">

Amazon Virtual Private Cloud (VPC) allows the users to use AWS resources in a virtual network. The users can customize their virtual networking environment as they like, such as selecting own IP address range, creating subnets, and configuring route tables and network gateways. The list of AWS services that can be used with Amazon VPC are :-
1. Amazon EC2
2. Amazon Route 53
3. Amazon WorkSpaces
4. Auto Scaling
5. Elastic Load Balancing
6. AWS Data Pipeline
7. Elastic Beanstalk
8. Amazon Elastic Cache
9. Amazon EMR
10. Amazon OpsWorks
11. Amazon RDS
12. Amazon Redshift

VPC actually Provides NaaS(Network-as-a-Service). In VPC world it is known as Subnets. In AWS, VPC provides Boundary to isolate our infrastructure.

#### Note:- If our instances are running on different Data-Center but they have the same VPC, they will have high-speed Connectivity. When we create AWS Account, by default they create a VPC and three Subnets for us and launch each Subnet in each Data-Center for disaster Recovery.

# AWS Subnets

<img src="images/subnet.png">

A default Subnet is a public subnet, because the main route table sends the subnet's traffic that is destined for the internet to the internet gateway. You can make a default subnet into a private subnet by removing the route from the destination 0.0.0.0/0 to the internet gateway. However, if you do this, no EC2 instance running in that subnet can access the internet.

Instances that you launch into a default subnet receive both a public IPv4 address and a private IPv4 address, and both public and private DNS hostnames. Instances that you launch into a nondefault subnet in a default VPC don't receive a public IPv4 address or a DNS hostname. You can change your subnet's default public IP addressing behavior.

## Public Subnets
A public subnet has an outbound route that sends all traffic through what AWS calls an Internet Gateway (IGW). The IGW lets traffic — IPv4 or IPv6 — out of the VPC without any constraints on bandwidth. Instances in public subnets can also receive inbound traffic through the IGW as long as their security groups and Network-ACLs allow it.

## Private Subnets
Contrast that with a private subnet which, if it needs to talk to the internet, must do so through a NAT(Network Access Translation) gateway. NATs are really common. Run a wireless router? The router itself does network address translation. Importantly a NAT won’t allow inbound traffic from the internet — that’s what makes a private subnet, well, private.

So what's the difference between Public Subnet and Private Subnet?

A <strong> public subnet </strong> has a route table that says, “send all outbound traffic (anything to the CIDR block 0.0.0.0/0) via this internet gateway.” A <strong> private subnet </strong> either does not allow outbound traffic to the internet or has a route that says, “send all outbound traffic via this NAT gateway.”

It’s important to note that all subnets in a VPC can talk to one another as long as the host’s security groups allow it. There’s always a route that says “keep traffic to {YourVPCsCIDRblock} inside the VPC.”
