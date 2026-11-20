
# Project 7: AWS Application Load Balancer (ALB)

## Project Overview
This project demonstrates how to deploy an Application Load Balancer (ALB) to distribute incoming HTTP traffic across three Amazon EC2 instances running Apache HTTP Server (HTTPD).

The objective is to improve availability and demonstrate how AWS distributes incoming web requests across multiple backend servers through a single entry point.

## Project Objectives
- Launch and configure three Amazon EC2 instances.
- Install and configure Apache HTTP Server (HTTPD) on each EC2 instance.
- Create unique webpages on each EC2 instance to identify which server responds.
- Create and configure an Application Load Balancer.
- Create a Target Group and register three EC2 instances.
- Configure health checks to monitor instance availability.
- Configure Security Groups to control traffic between the ALB and EC2 instances.
- Test traffic distribution through the ALB DNS name.
- Observe how the ALB handles unhealthy targets.

## AWS Services Used
- Amazon EC2
- Application Load Balancer (ALB)
- Target Groups
- Amazon VPC
- Security Groups
- Apache HTTP Server (HTTPD)

## Architecture
Internet
   |
   v
Application Load Balancer (ALB)
   |
   v
Target Group
   |
   |-------- EC2 Instance 1 (Apache HTTPD)
   |
   |-------- EC2 Instance 2 (Apache HTTPD)
   |
   |-------- EC2 Instance 3 (Apache HTTPD)

## Implementation

### 1. Launch EC2 Instances
- Launched three EC2 instances.
- Used Amazon Linux as the operating system.
- Configured the required networking and Security Groups.

### 2. Install Apache HTTP Server
Installed Apache HTTP Server on each EC2 instance.

```bash
sudo yum update -y
sudo yum install -y httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```

### 3. Configure Webpages
Created a unique webpage on each EC2 instance to identify which server is responding.

**EC2 Instance 1:**
```bash
echo "<h1>Hello Universe from Server 1</h1>" | sudo tee /var/www/html/index.html
```

**EC2 Instance 2:**
```bash
echo "<h1>Hello Universe from Server 2</h1>" | sudo tee /var/www/html/index.html
```

**EC2 Instance 3:**
```bash
echo "<h1>Hello Universe from Server 3</h1>" | sudo tee /var/www/html/index.html
```

### 4. Create Target Group
- Created a Target Group for the EC2 instances.
- Configured HTTP traffic on Port 80.
- Registered all three EC2 instances.
- Configured health checks to monitor the availability of the instances.

### 5. Create Application Load Balancer
- Created an internet-facing Application Load Balancer.
- Configured the ALB to listen on HTTP Port 80.
- Forwarded incoming requests to the Target Group.
- Configured Security Groups to allow HTTP traffic to the ALB and permit backend traffic from the ALB Security Group to the EC2 instances.

### 6. Testing
- Verified Apache HTTP Server was running on all three EC2 instances.
- Tested the webpages locally using `curl localhost`.
- Verified all three EC2 instances were registered in the Target Group.
- Confirmed the health status of the registered targets.
- Accessed the website using the ALB DNS name.
- Observed responses from different EC2 instances through the ALB.
- Tested how the ALB handles unhealthy targets.

## Key Learnings
- Understanding how Application Load Balancers distribute incoming traffic.
- Configuring Target Groups and health checks.
- Deploying multiple EC2 instances to serve web requests.
- Configuring Security Groups for secure communication between ALB and backend instances.
- Understanding the importance of high availability and load balancing.
- Troubleshooting web server and networking configurations.

## Conclusion
This project provided hands-on experience in deploying an Application Load Balancer with three EC2 instances running Apache HTTP Server.

By configuring Target Groups, health checks and Security Groups, I gained a better understanding of how AWS distributes incoming traffic across multiple backend servers and how load balancing contributes to availability and scalable cloud infrastructure.
