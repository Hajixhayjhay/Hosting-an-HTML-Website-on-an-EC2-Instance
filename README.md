# Hosting-an-HTML-Website-on-an-EC2-Instance# README: EC2 Website Deployment

## Project Overview
This project showcases the successful deployment of a static HTML website on AWS EC2 instances using a robust reference architecture. The deployment emphasizes high availability, fault tolerance, security, and scalability, utilizing various AWS services to achieve a production-ready solution.

## Architecture Summary
The website is hosted on EC2 instances within a secure VPC setup that includes public and private subnets across two availability zones (AZs) to ensure high availability and fault tolerance. The key components of the architecture are:

### VPC Configuration
- **Public and Private Subnets:** Configured in two availability zones to enhance redundancy and availability.
- **Internet Gateway:** Enables communication between the VPC and the internet.
- **NAT Gateway:** Allows instances in private subnets to securely access the internet.
- **Bastion Host:** Provides secure SSH access to instances in private subnets.

### Compute Resources
- **EC2 Instances:** Deployed in private subnets to host the website. These instances are managed through an Auto Scaling Group to ensure scalability and reliability.
- **Auto Scaling Group:** Automatically adjusts the number of EC2 instances based on traffic demands to maintain performance and availability.

### Networking and Security
- **Application Load Balancer (ALB):** Distributes incoming traffic across multiple EC2 instances to ensure load balancing and fault tolerance.
- **Security Groups:** Configured to control inbound and outbound traffic, enhancing the overall security posture.

### Domain Name and DNS
- **Route 53:** A custom domain name was registered and a record set was created to point the domain to the Application Load Balancer.

### Secure Communication
- **HTTPS:** SSL/TLS certificates were configured on the ALB to enable secure communication to the website.

## Deployment Process
1. **VPC Setup:**
   - Created a VPC with both public and private subnets in two availability zones.
   - Attached an Internet Gateway to the VPC for external communication.
   - Configured NAT Gateways in public subnets to allow private instances to access the internet.

2. **EC2 Instances and Auto Scaling:**
   - Created a launch template to define the configuration of EC2 instances.
   - Set up an Auto Scaling Group to manage EC2 instances dynamically based on traffic patterns.

3. **Application Load Balancer:**
   - Deployed an ALB in the public subnets to distribute traffic across the EC2 instances.

4. **Domain Name Setup:**
   - Registered a domain name using Route 53.
   - Created a record set to map the domain to the ALB for seamless access.

5. **Secure Communication:**
   - Configured SSL/TLS certificates on the ALB to enable HTTPS.

6. **Website Files Deployment:**
   - Stored the website files in a GitHub repository.
   - Configured the deployment script to automatically download and deploy the files from the GitHub repository to the EC2 instances.

## Deployment Script
Below is the Bash script used to automate the deployment of the website on EC2 instances:

```bash
#!/bin/bash
sudo su
yum update -y
yum install -y httpd
cd /var/www/html
yum install git -y
wget https://github.com/Hajixhayjhay/Hosting-an-HTML-Website-on-an-EC2-Instance.git
git clone https://github.com/Hajixhayjhay/Hosting-an-HTML-Website-on-an-EC2-Instance.git
cp -r Hosting-an-HTML-Website-on-an-EC2-Instance/techmax.zip /var/www/html
unzip techmax.zip
cp -r techmax/* /var/www/html
rm -rf techmax techmax.zip
rm -rf Hosting-an-HTML-Website-on-an-EC2-Instance Hosting-an-HTML-Website-on-an-EC2-Instance.git
systemctl enable httpd
systemctl start httpd
```

### Explanation of the Deployment Script
1. **`#!/bin/bash`**: Specifies that the script should be executed using the Bash shell.
2. **`sudo su`**: Switches to the root user to ensure all commands are executed with administrative privileges.
3. **`yum update -y`**: Updates all packages on the instance to their latest versions.
4. **`yum install -y httpd`**: Installs the Apache web server (httpd).
5. **`cd /var/www/html`**: Changes the directory to the default web root where the website files will be stored.
6. **`yum install git -y`**: Installs Git to enable downloading files from a GitHub repository.
7. **`wget https://github.com/Hajixhayjhay/Hosting-an-HTML-Website-on-an-EC2-Instance.git`**: Downloads the GitHub repository using `wget`.
8. **`git clone https://github.com/Hajixhayjhay/Hosting-an-HTML-Website-on-an-EC2-Instance.git`**: Clones the repository to the local system.
9. **`cp -r Hosting-an-HTML-Website-on-an-EC2-Instance/techmax.zip /var/www/html`**: Copies the `techmax.zip` file to the web root.
10. **`unzip techmax.zip`**: Unzips the `techmax.zip` file to extract the website files.
11. **`cp -r techmax/* /var/www/html`**: Copies all extracted files to the web root directory.
12. **`rm -rf techmax techmax.zip`**: Removes the extracted folder and zip file to clean up.
13. **`rm -rf Hosting-an-HTML-Website-on-an-EC2-Instance Hosting-an-HTML-Website-on-an-EC2-Instance.git`**: Removes the cloned GitHub repository to save space.
14. **`systemctl enable httpd`**: Enables the Apache web server to start on boot.
15. **`systemctl start httpd`**: Starts the Apache web server.

## Key Achievements
- **High Availability:** Achieved by deploying resources across two availability zones.
- **Fault Tolerance:** Ensured through automatic failover using the Application Load Balancer and Auto Scaling Group.
- **Scalability:** The Auto Scaling Group dynamically adjusts the number of EC2 instances based on traffic demands.
- **Security:** Enhanced by hosting instances in private subnets, configuring security groups, and enabling HTTPS.
- **Custom Domain:** Successfully registered a custom domain name with Route 53, making the website accessible via a user-friendly URL.

## Tools and Services Used
- **Amazon VPC**
- **Internet Gateway**
- **NAT Gateway**
- **Bastion Host**
- **EC2 Instances**
- **Auto Scaling Group**
- **Application Load Balancer**
- **Route 53**
- **SSL/TLS Certificates**
- **GitHub Repository**

## Conclusion
The project demonstrates a complete and successful deployment of a static website using AWS best practices. The implemented architecture ensures high availability, fault tolerance, security, and scalability. The website is accessible via a custom domain with secure HTTPS communication, providing a seamless and secure user experience.


