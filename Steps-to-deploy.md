## Deploying phpMyAdmin in AWS VPC ##

This repository contains instructions and configurations for deploying phpMyAdmin within an AWS Virtual Private Cloud (VPC). This setup includes a web server, backend application, and a MySQL database instance.

## Overview

The deployment involves:

Creating a VPC with public and private subnets.

Setting up a NAT Gateway and Internet Gateway.

Deploying EC2 instances for web and backend applications.

Configuring an RDS MySQL instance.

Installing and configuring phpMyAdmin on an EC2 instance.

## Steps to Deploy
1. Created a Virtual Private Cloud (VPC)

2. Configure Subnets

• Create one public subnet for the web server.

• Create three private subnets:

One for the backend application & Two for the database instances.

3. Configure Route Tables

Create a route table for the public subnet and associate it with the internet gateway.

Create a route table for the private subnets and associate it with the NAT gateway for outbound traffic.

4. Set Up NAT Gateway

Create a NAT Gateway in the public subnet to enable outbound internet traffic from the private subnets.

Update the route table for the private subnets to route traffic through the NAT Gateway.

5. Create and Attach an Internet Gateway

Create an Internet Gateway and attach it to the VPC.

Update the route table for the public subnet to route internet traffic through the Internet Gateway.

6. Launch EC2 Instances

Web Server Instance:
    
Launch an EC2 instance in the public subnet, Install and configure an HTTPD web server.
    
Backend EC2 Instance:
    
Launch an EC2 instance in one of the private subnets, Install and configure HTTPD & phpMyAdmin on backend instance.

7. Set Up RDS MySQL Instance

Create an RDS MySQL instance in one of the private subnets.

Configure the security group to allow connections from the backend EC2 instance.

8. Configure phpMyAdmin

Access phpMyAdmin on the backend EC2 instance.

Link phpMyAdmin to the RDS MySQL instance using the RDS endpoint.

9. Configure Load Balancer

Due to cost considerations, a load balancer was not created in this setup. However, I have understood how Application Load Balancer (ALB) works and configuring target groups if needed.
