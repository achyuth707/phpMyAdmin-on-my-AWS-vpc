Steps to deploy phpMyAdmin Application in AWS VPC.

AWS Documentation I have referred to Install phpMyAdmin - https://docs.aws.amazon.com/linux/al2/ug/ec2-lamp-amazon-linux-2.html#prepare-lamp-server

    VPC Creation: 
          Created a Virtual Private Cloud (VPC).
    
    Subnets:
          1 Public Subnet: For the web server.
          3 Private Subnets: 1 for the backend application & 2 for the database.

    Route Tables: 
        Configured and updated route tables for both public and private routes, ensuring proper subnet associations for efficient routing.
        
    NAT Gateway: 
        Created a NAT gateway in the public subnet to enable outbound internet traffic from instances in the private subnets. (Note: This will incur charges as it is not covered under the free tier limits).
        
    Internet Gateway: 
        Created and attached an Internet gateway to the public subnet routes to enable internet access.
        
    EC2 and RDS Instances:
        Web Server (Public Subnet): Installed and configured an HTTPD web server on an EC2 instance in the public subnet.
        Backend EC2 Instance (Private Subnet): Installed and configured HTTPD and phpMyAdmin on an EC2 instance in one of the private subnets.
        
    RDS MySQL Instance:
        Created a free tier RDS MySQL instance and linked the endpoint to the phpMyAdmin application.
        
    Load Balancer: A load balancer was not created due to cost considerations, as it would exceed the free tier limits, But I understood the concept on how to create ALB and configuring the target groups to the loadbalancer.
