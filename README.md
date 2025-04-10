# AWS Auto Scaling and Load Balancer Deployment using Terraform

This project sets up a scalable and highly available web infrastructure on AWS using Terraform. It provisions an Application Load Balancer (ALB), an Auto Scaling Group (ASG), a Launch Template, and EC2 instances that automatically scale and serve traffic using Apache.

## Overview

The infrastructure includes:

- **Launch Template**: Defines EC2 instance configuration, including AMI, instance type, key pair, security groups, and a user data script that installs Apache and serves a custom HTML message.
- **Auto Scaling Group**: Automatically maintains the desired number of EC2 instances. Configured with a minimum of 1, maximum of 3, and default desired capacity of 2.
- **Application Load Balancer**: Distributes incoming HTTP traffic across healthy instances in multiple availability zones.
- **Security Group**: Allows inbound traffic on ports 22 (SSH) and 80 (HTTP).
- **Key Pair**: Enables SSH access to EC2 instances, configured at the launch template level.

## Files Included

- `main.tf`: Main Terraform configuration file containing all resource definitions.
- `variables.tf`: Defines input variables (e.g., key pair name).
- `outputs.tf`: Displays the ALB DNS name after deployment.
- `.gitignore`: Ensures large and unnecessary files are excluded from version control.

## Requirements

- Terraform installed locally
- AWS account with credentials configured (via CLI or environment variables)
- An existing EC2 key pair in your chosen AWS region (e.g., `us-west-1`)

## Deployment

1. Clone the repository:
   ```bash
   git clone https://github.com/amirValiulla32/aws-auto-scaling.git
   cd aws-auto-scaling
2. Initialize Terraform:
   ```bash
   terraform init
3. Apply the configuration:
   ```bash
   terraform apply -var="key_name=your-ec2-keypair-name"
4. After deployment, Terraform will output the Load Balancer DNS name:

   ```hcl
   alb_dns = "app-lb-1234567890.us-west-1.elb.amazonaws.com"
5. Visit the URL in your browser. You should see a message like:

   ```text
   Hello from ip-172-31-xx-xx.us-west-1.compute.internal

