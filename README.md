
# Deploying a Static Website on AWS EC2

This project demonstrates how to set up a Linux server on AWS EC2 and deploy a simple static website. Below are the steps I followed to complete this project.

---

## Requirements
- **AWS Account**: Created and configured an AWS account.
  - Logged in through the root account or IAM user.
  - Created a key pair for secure SSH access.
- **Instance Specifications**:
  - **AMI**: Ubuntu Server
  - **Instance Type**: t3.micro (Free Tier eligible)
  - **Network**: Default VPC and subnet for your region
  - **Inbound Rules**: Allowed traffic on ports 22 (SSH) and 80 (HTTP)
  - **Key Pair**: Created a new key pair for SSH access
  - **Public IP**: Assigned a public IP address to the instance

---

## Steps Taken

### 1. Launching an EC2 Instance
- Navigated to the AWS Management Console and launched a new EC2 instance with the specified configurations.
- Configured the security group to allow:
  - SSH (port 22) for remote access.
  - HTTP (port 80) for web traffic.

### 2. Connecting to the Instance via SSH
- Used the private key file downloaded from AWS to connect to the instance:
  ```bash
  ssh -i <path-to-private-key> ubuntu@<public-ip>
  ```
  Alternatively:
  - Accessed the instance through:
    ```bash
    ssh -i ".pem file" ubuntu@<public-ip>
    ```
  - Accessed the EC2 instance console through HTTP, added my public key to the instance at `~/.ssh/authorized_keys`, and connected using:
    ```bash
    ssh -i "id_rsa" ubuntu@<public-ip>
    ```
  - Created an SSH configuration file for simplified access with an alias and connected using:
    ```bash
    ssh <alias>
    ```

### 3. Updating System Packages
- Updated the instance's package list and installed necessary updates:
  ```bash
  sudo apt update
  sudo apt upgrade -y
  ```

### 4. Installing a Web Server
- Installed Nginx as the web server:
  ```bash
  sudo apt install nginx -y
  ```
- Verified that Nginx was running by visiting the public IP address in a browser.

### 5. Creating a Static Website
- Created a simple HTML file for the website:
  ```bash
  cd /var/www/html/
  
  echo "<!DOCTYPE html>
  <html>
  <head><title>My Static Website</title></head>
  <body>
  <h1>Welcome to My Static Website</h1>
  <p>This site is hosted on AWS EC2!</p>
  </body>
  </html>" >> index.html
  ```

### 6. Deploying the Website
- Restarted the Nginx service to ensure the new HTML file was served:
  ```bash
  sudo systemctl restart nginx
  ```
- Accessed the static website using the EC2 instance's public IP address.

---


This project is part of [Janis Adhikari's](https://roadmap.sh/projects/ec2-instance)  DevOps projects.