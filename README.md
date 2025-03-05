# Auto Scaling Lab
## Objective

This project demonstrates automatic scaling using **AWS CloudFormation** to deploy an **Apache web server** that dynamically adjusts its capacity based on CPU load. When an instance exceeds a **50% CPU utilization threshold**, the **Auto Scaling Group (ASG)** launches a new instance to distribute traffic. Each instance responds with its unique **IP address** and **instance ID**, verifying proper load distribution.

## Features

- **Auto Scaling Group (ASG)** that automatically scales based on CPU utilization.
- **Apache Web Server** that displays the instance’s IP address and instance ID.
- **Interactive button** on the webpage to artificially stress the CPU of the hosting instance.
- **Application Load Balancer (ALB)** distributes traffic across instances in a round-robin fashion.
- **Private Subnet** to securely host instances.
- **Public Subnet** to deploy the Application Load Balancer.
- **CloudFormation Template** that defines and deploys resources including ASG, scaling policies, load balancer, subnets, and more.

## Tasks

### 1. **Auto Scaling Group (ASG) Configuration**

- **Minimum Capacity:** 1 instance.
- **Desired Capacity:** 1 instance.
- **Maximum Capacity:** 3 instances.
- **Scaling Policy:** Triggers a scale-out action when the CPU utilization exceeds 50%. Automatic scale down as well when the usage falls below 35%

### 2. **Apache Web Server**

- Displays a message in the format: 
  ```
  Hello from [IP Address] / [Instance ID]
  ```
- Includes an interactive "Stress CPU" button on the webpage that, when clicked, artificially stresses the CPU of the hosting instance.

### 3. **Networking Setup**

- **Private Subnet:** Hosts the Apache web server instances securely.
- **Public Subnet:** Hosts the Application Load Balancer (ALB) to distribute incoming traffic.

### 4. **Deployment Automation**

- **AWS CloudFormation Git Sync** is used for automating deployment.
- The **CloudFormation template** defines all the necessary resources: ASG, scaling policies, load balancer, subnets, and more.
- EC2 **User Data** is used to install the **Apache Web Server** and the web application.


## Testing

- Visit [http://asg-lab-alb-1531434573.eu-north-1.elb.amazonaws.com/](http://asg-lab-alb-1531434573.eu-north-1.elb.amazonaws.com/)
- When the page is refreshed, the same IP address and Instance ID would be displayed because there is only one EC2 instance running
- When the "Stress CPU" button is clicked a few times, the CPU utilization would rise above the threshold (50%) which triggers the Auto Scaling Group to launch additional instances. This can take up to 3 minutes for the instance to be fully provisioned
- Now, refresh the page and alternating IP addresses would be displayed
