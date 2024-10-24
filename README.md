---

# Static Website Hosted on AWS EC2

This project demonstrates how to deploy a static HTML web application on AWS using EC2 instances. The infrastructure is designed for high availability, scalability, security, and fault tolerance. Below is an overview of the architecture and resources used.

## Project Overview

### Key AWS Services Utilized:
1. **Virtual Private Cloud (VPC)** - A VPC was configured with both public and private subnets across two availability zones for enhanced fault tolerance.
2. **Internet Gateway** - Allows instances in the VPC to connect to the internet.
3. **Security Groups** - Network firewall settings were established to control traffic to and from the instances.
4. **Availability Zones** - Two availability zones were leveraged for high availability and redundancy.
5. **Public Subnets** - These hosted resources such as the NAT Gateway and Application Load Balancer.
6. **EC2 Instance Connect Endpoint** - Secure connections were enabled to resources in both public and private subnets.
7. **Private Subnets** - Web servers were deployed in private subnets for enhanced security.
8. **NAT Gateway** - Instances in private subnets were allowed internet access via a NAT Gateway.
9. **EC2 Instances** - The website was hosted on EC2 instances.
10. **Application Load Balancer (ALB)** - Even distribution of traffic across multiple EC2 instances in an Auto Scaling Group.
11. **Auto Scaling Group** - Automatic management of EC2 instances for availability, scalability, fault tolerance, and elasticity.
12. **GitHub** - Web files were stored in a GitHub repository for version control.
13. **AWS Certificate Manager (ACM)** - Secured communication using SSL certificates.
14. **Simple Notification Service (SNS)** - Set up notifications to monitor Auto Scaling activities.
15. **Route 53** - Registered the domain and configured DNS settings.

### Architecture Diagram
The architecture diagram for this setup can be found in the project's GitHub repository.

## Getting Started

### Prerequisites
- AWS account with permissions to create and configure VPC, EC2, and related services.
- Domain name registered via Route 53 (or another domain registrar).
- Git installed on your local machine for cloning the repository.
- SSL certificate configured in AWS Certificate Manager.

### Deployment Steps

1. **VPC Setup**: 
   - Configure a VPC with public and private subnets across two availability zones.
   - Deploy an Internet Gateway to connect the VPC to the internet.
   - Set up appropriate security groups to control traffic.

2. **EC2 Instances**:
   - Launch EC2 instances in private subnets for hosting the web application.
   - Ensure instances can access the internet using a NAT Gateway.

3. **Application Load Balancer**:
   - Set up an Application Load Balancer in public subnets for distributing traffic.
   - Register the EC2 instances with the Load Balancer through a target group.

4. **Auto Scaling**:
   - Configure an Auto Scaling Group to manage the number of EC2 instances based on traffic.

5. **DNS and SSL**:
   - Use Route 53 to register your domain and set up DNS routing.
   - Secure the website using AWS Certificate Manager (ACM) for SSL encryption.

6. **Monitoring and Notifications**:
   - Set up SNS to send alerts on Auto Scaling activities.

### Installation on EC2 Instances

Below is a script to automate the installation and setup of a static web app on an EC2 instance.

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
git clone https://github.com/Pedro-marques03/host-a-static-website-on-aws/

# Copy all files, including hidden ones, from the cloned repository to the Apache web root
cp -R host-a-static-website-on-aws/. /var/www/html/

# Remove the cloned repository directory to clean up unnecessary files
rm -rf host-a-static-website-on-aws

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

### Conclusion
This project demonstrates a comprehensive approach to hosting a static website on AWS using EC2, VPC, Load Balancing, Auto Scaling, and other AWS services. For further details, including the reference architecture diagram and scripts, please visit the [GitHub repository](https://github.com/Pedro-marques03/host-a-static-website-on-aws/).

---
