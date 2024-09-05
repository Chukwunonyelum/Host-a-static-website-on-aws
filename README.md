---

# Host a Static Website on AWS

This project demonstrates how to host a static HTML web application on AWS, utilizing various AWS services and resources to ensure scalability, security, and high availability. The website is hosted on EC2 instances, with infrastructure configured for resilience, fault tolerance, and automated scaling.

## Project Overview

The project involves deploying a static website on AWS using the following AWS resources:

1. **Virtual Private Cloud (VPC)**: Configured with both public and private subnets across two different availability zones.
2. **Internet Gateway**: Deployed to facilitate connectivity between VPC instances and the wider Internet.
3. **Security Groups**: Established as a network firewall mechanism to control inbound and outbound traffic.
4. **Multi-AZ Deployment**: Leveraged two Availability Zones to enhance system reliability and fault tolerance.
5. **Public Subnets**: Used for infrastructure components like the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint**: Implemented for secure connections to assets within both public and private subnets.
7. **Private Subnets**: Used to position web servers (EC2 instances) for enhanced security.
8. **NAT Gateway**: Enabled instances in both the private application and data subnets to access the Internet securely.
9. **EC2 Instances**: Hosted the website on these instances within private subnets.
10. **Application Load Balancer (ALB)**: Employed along with a target group to evenly distribute web traffic to an Auto Scaling Group of EC2 instances across multiple Availability Zones.
11. **Auto Scaling Group**: Utilized to automatically manage EC2 instances, ensuring website availability, scalability, fault tolerance, and elasticity.
12. **GitHub**: Used to store web files for version control and collaboration.
13. **AWS Certificate Manager**: Secured application communications with SSL/TLS certificates.
14. **Amazon Simple Notification Service (SNS)**: Configured to send alerts about activities within the Auto Scaling Group.
15. **Amazon Route 53**: Registered the domain name and set up DNS records for the application.

## Architecture Diagram

Refer to the architecture diagram in the repository to visualize the infrastructure setup.

## Prerequisites

- AWS Account with appropriate permissions.
- Domain registered and DNS configured in Amazon Route 53.
- GitHub account for storing the web files and scripts.
- Basic understanding of AWS services and CLI.

## Deployment Steps

### 1. Setting Up the AWS Infrastructure

1. **Create a VPC** with public and private subnets across two availability zones.
2. **Deploy an Internet Gateway** and attach it to the VPC.
3. **Configure Security Groups** to allow required inbound and outbound traffic.
4. **Set up a NAT Gateway** in a public subnet to enable internet access for private subnet instances.
5. **Deploy EC2 Instances** in private subnets to host the web application.
6. **Set up an Application Load Balancer** in public subnets to distribute incoming traffic across EC2 instances.
7. **Configure an Auto Scaling Group** to manage the number of EC2 instances automatically based on traffic.
8. **Register your domain** and set up DNS records using Amazon Route 53.
9. **Secure the website** using AWS Certificate Manager to handle SSL certificates.

### 2. Launch EC2 Instances and Deploy the Web Application

Use the provided Bash script to set up the EC2 instances and deploy the static web application.

### Deployment Script

The following script installs necessary packages, clones the web files from GitHub, and configures the Apache server to host the website:

```bash
#!/bin/bash

# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Install Git
yum install git -y

# Clone the project GitHub repository to the current directory
git clone https://github.com/aosnotes77/host-a-static-website-on-aws.git

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### 3. Configure Auto Scaling and Monitoring

1. **Configure Auto Scaling policies** to automatically scale the number of EC2 instances based on CPU utilization or other metrics.
2. **Set up CloudWatch Alarms** and integrate them with Amazon SNS for monitoring and alerts.

## Conclusion

This setup provides a robust, scalable, and secure environment for hosting a static website on AWS, leveraging the best practices of AWS architecture to ensure high availability and fault tolerance.

