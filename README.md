# CloudFormation Template for Web Application Deployment

## Description

This CloudFormation template is designed to deploy infrastructure for a web application on AWS. It includes the creation of a Virtual Private Cloud (VPC), subnets, route tables, NAT gateways, security groups, launch templates, and auto-scaling groups.

## Components

### 1. VPC and Subnets

- **MyVPC**: Creates a Virtual Private Cloud (VPC) with a specified CIDR block.
- **PublicSubnet1 and PublicSubnet2**: Creates public subnets in two availability zones. These subnets have routes via an internet gateway.
- **PrivateSubnet1 and PrivateSubnet2**: Creates private subnets in two availability zones. These subnets have routes via a NAT gateway for internet access.

### 2. Internet Gateway and NAT Gateway

- **InternetGateway**: Creates an internet gateway to provide internet access.
- **NatGateway1**: Creates a NAT gateway to provide internet access for private subnets.

### 3. Route Tables

- **PublicRouteTable**: Route table for public subnets with a default route through the internet gateway.
- **PrivateRouteTable1**: Route table for private subnets with a default route through the NAT gateway.

### 4. Security Group

- **MySecurityGroup**: Creates a security group with rules allowing access to ports 22 (SSH) and 80 (HTTP).

### 5. Launch Template

- **MyLaunchTemplate**: Defines a launch template for EC2 instances with settings such as AMI, instance type, SSH key, and user data. The user data script installs an HTTPD server and sets up a welcome page.

### 6. Load Balancer and Target Group

- **MyTargetGroup**: Creates a target group for the load balancer with HTTP health checks.
- **MyELB**: Creates an internet-facing load balancer.
- **MyListener**: Configures a listener for the load balancer that forwards traffic to the target group.

### 7. Auto Scaling Group

- **MyAutoScalingGroup1**: Creates an auto-scaling group with a minimum of 2 instances, a maximum of 4 instances, and a desired capacity of 2.

## Parameters

- **EnvironmentName**: The name of the environment, which is prefixed to resource names.
- **VpcCIDR**: The CIDR block for the VPC.
- **PublicSubnet1CIDR**: CIDR block for the first public subnet.
- **PublicSubnet2CIDR**: CIDR block for the second public subnet.
- **PrivateSubnet1CIDR**: CIDR block for the first private subnet.
- **PrivateSubnet2CIDR**: CIDR block for the second private subnet.
- **InstanceTypeKyial**: The EC2 instance type to be used.
- **TypeELB**: The type of load balancer (application, network, or gateway).

## Outputs

- **LoadBalancerUrl**: The URL of the Application Load Balancer.
- **VPC**: A reference to the created VPC.
- **PublicSubnets**: A list of the public subnets.
- **PrivateSubnets**: A list of the private subnets.
- **PublicSubnet1**: A reference to the first public subnet.
- **PublicSubnet2**: A reference to the second public subnet.
- **PrivateSubnet1**: A reference to the first private subnet.
- **PrivateSubnet2**: A reference to the second private subnet.
- **MySecurityGroup**: The security group with the specified rules.


