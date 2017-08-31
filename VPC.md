# Amazon Virtual Private Cloud (VPC)

Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the Amazon Web Services (AWS) cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.  You can use both IPv4 and IPv6 in your VPC for secure and easy access to resources and applications.
 

You can easily customize the network configuration for your Amazon Virtual Private Cloud. For example, you can create a public-facing subnet for your webservers that has access to the Internet, and place your backend systems such as databases or application servers in a private-facing subnet with no Internet access. You can leverage multiple layers of security, including security groups and network access control lists, to help control access to Amazon EC2 instances in each subnet.

Additionally, you can create a Hardware Virtual Private Network (VPN) connection between your corporate datacenter and your VPC and leverage the AWS cloud as an extension of your corporate datacenter.

## Features and Benefits

### Multiple Connectivity Options
A variety of connectivity options exist for your Amazon Virtual Private Cloud. You can connect your VPC to the Internet, to your datacenter, or other VPC's, based on the AWS resources that you want to expose publicly and those that you want to keep private.

- Connect directly to the Internet (public subnets)– You can launch instances into a publicly accessible subnet where they can send and receive traffic from the Internet.
- Connect to the Internet using Network Address Translation (private subnets)– Private subnets can be used for instances that you do not want to be directly addressable from the Internet. Instances in a private subnet can access the Internet without exposing their private IP address by routing their traffic through a Network Address Translation (NAT) gateway in a public subnet.
- Connect securely to your corporate datacenter– All traffic to and from instances in your VPC can be routed to your corporate datacenter over an industry standard, encrypted IPsec hardware VPN connection.
- Connect privately to other VPCs- Peer VPCs together to share resources across multiple virtual networks owned by your or other AWS accounts.
- Connect to Amazon S3 without using an internet gateway or NAT, and control what resources, requests, or users are allowed through a VPC endpoint.
- Combine connectivity methods to match the needs of your application– You can connect your VPC to both the Internet and your corporate datacenter and configure Amazon VPC route tables to direct all traffic to its proper destination.

### Secure

Amazon VPC provides advanced security features such as security groups and network access control lists to enable inbound and outbound filtering at the instance level and subnet level. In addition, you can store data in Amazon S3 and restrict access so that it’s only accessible from instances in your VPC. Optionally, you can also choose to launch Dedicated Instances which run on hardware dedicated to a single customer for additional isolation.

### Simple

You can create a VPC quickly and easily using the AWS Management Console. You can select one of the common network setups that best match your needs and press "Start VPC Wizard." Subnets, IP ranges, route tables, and security groups are automatically created for you, so you can concentrate on creating the applications to run in your VPC.

### All the Scalability and Reliability of AWS

Amazon VPC provides all the same benefits as the rest of the AWS platform. You can instantly scale your resources up or down, select Amazon EC2 instances types and sizes that are right for your applications, and pay only for the resources you use - all within Amazon’s proven infrastructure.

## Use Cases

### Host a simple, public-facing website

You can host a basic web application, such as a blog or simple website in a VPC, and gain the additional layers of privacy and security afforded by Amazon VPC. You can help secure the website by creating security group rules which allow the webserver to respond to inbound HTTP and SSL requests from the Internet while simultaneously prohibiting the webserver from initiating outbound connections to the Internet. You can create a VPC that supports this use case by selecting "VPC with a Single Public Subnet Only" from the Amazon VPC console wizard.

### Host multi-tier web applications

You can use Amazon VPC to host multi-tier web applications and strictly enforce access and security restrictions between your webservers, application servers, and databases. You can launch webservers in a publicly accessible subnet and application servers and databases in non-publically accessible subnets. The application servers and databases can’t be directly accessed from the Internet, but they can still access the Internet via a NAT gateway to download patches, for example. You can control access between the servers and subnets using inbound and outbound packet filtering provided by network access control lists and security groups. To create a VPC that supports this use case, you can select "VPC with Public and Private Subnets" in the Amazon VPC console wizard.
Host scalable web applications in the AWS cloud that are connected to your datacenter
You can create a VPC where instances in one subnet, such as webservers, communicate with the Internet while instances in another subnet, such as application servers, communicate with databases on your corporate network. An IPsec VPN connection between your VPC and your corporate network helps secure all communication between the application servers in the cloud and databases in your datacenter. Webservers and application servers in your VPC can leverage Amazon EC2 elasticity and Auto Scaling features to grow and shrink as needed. You can create a VPC to support this use case by selecting "VPC with Public and Private Subnets and Hardware VPN Access" in the Amazon VPC console wizard.

### Extend your corporate network into the cloud

You can move corporate applications to the cloud, launch additional webservers, or add more compute capacity to your network by connecting your VPC to your corporate network. Because your VPC can be hosted behind your corporate firewall, you can seamlessly move your IT resources into the cloud without changing how your users access these applications. You can select "VPC with a Private Subnet Only and Hardware VPN Access" from the Amazon VPC console wizard to create a VPC that supports this use case.

### Disaster Recovery

You can periodically backup your mission critical data from your datacenter to a small number of Amazon EC2 instances with Amazon Elastic Block Store (EBS) volumes, or import your virtual machine images to Amazon EC2. In the event of a disaster in your own datacenter, you can quickly launch replacement compute capacity in AWS to ensure business continuity. When the disaster is over, you can send your mission critical data back to your datacenter and terminate the Amazon EC2 instances that you no longer need. By using Amazon VPC for disaster recovery, you can have all the benefits of a disaster recovery site at a fraction of the normal cost.

# Getting Started Guide

## Overview

A virtual private cloud (VPC) is a virtual network that closely resembles a traditional network that you'd operate in your own data center, with the benefits of using the scalable infrastructure of Amazon Web Services (AWS). After you complete the tasks in this exercise, you'll have an Amazon EC2 instance running in a VPC that you can access from the Internet using SSH (for Linux instances) or Remote Desktop (for Windows instances).

For an overview of Amazon VPC, see What is Amazon VPC? in the Amazon VPC User Guide.

The following diagram shows the architecture that you'll create as you complete the exercise in this guide. The security group that you set up and associate with the instance allows traffic only through specific ports, locking down communication with the instance according to the rules that you specify. Using an Elastic IP address (EIP) enables an instance in a VPC, which is otherwise private, to be reached from the Internet through an Internet gateway (for example, it could act as a web server).

## Getting Started With Amazon VPC

