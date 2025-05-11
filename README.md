# AWS Single-Instance Web Server Infrastructure

This Terraform configuration sets up a basic web server infrastructure in AWS with the following components:

## Architecture Overview

- **Region**: us-east-2 (Ohio)
- **VPC**: A custom VPC with CIDR block 10.0.0.0/16
- **Subnet**: A public subnet in availability zone us-east-2a
- **Internet Gateway**: Provides internet access to resources in the VPC
- **Route Table**: Routes traffic from the subnet to the internet gateway
- **Security Group**: Controls inbound and outbound traffic
- **EC2 Instance**: A t2.micro Ubuntu instance with Nginx installed

## Security Features

- Access is limited to HTTP (port 80) and SSH (port 22)
- Outbound traffic is allowed on all ports

## Prerequisites

1. AWS account with appropriate permissions
2. Terraform installed on your local machine
3. AWS CLI configured with access credentials
4. An SSH key pair named "server.kp" in your AWS account

## Deployment Instructions

1. Clone this repository
2. Initialize Terraform:
   ```
   terraform init
   ```
3. Review the execution plan:
   ```
   terraform plan
   ```
4. Apply the configuration:
   ```
   terraform apply
   ```
   
   ![Screenshot_11-5-2025_16141_potential-bassoon-v56v975jgxrfw467 github dev](https://github.com/user-attachments/assets/278a9187-4f31-4701-bf4e-6a0b9d8948f7)
   
6. Confirm by typing "yes" when prompted

## Accessing the Web Server

After deployment, the public IP address of the web server will be displayed as an output. You can access the Nginx default page by visiting:

```
http://<public_ip>
```

![Screenshot 2025-05-11 155614](https://github.com/user-attachments/assets/d770a481-9dde-4944-b6d9-b2ace8f3bb7e)

To SSH into the instance:

```
ssh -i path/to/server.kp.pem ubuntu@<public_ip>
```

## Clean Up

To destroy all resources created by this configuration:

```
terraform destroy
```

## Customization

- To change the region, modify the `region` parameter in the AWS provider block
- To use a different AMI, update the `ami` parameter in the EC2 instance resource
- To change the instance type, modify the `instance_type` parameter

## Notes

- The EC2 instance is provisioned with Nginx using a user_data script
- The instance is assigned a public IP address automatically
- The AMI used (ami-04f167a56786e4b09) is an Ubuntu image in the us-east-2 region
