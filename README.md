
# AWS Multi-Region Failover Using Global Accelerator

A single global endpoint that routes users to the nearest healthy AWS Region for better performance.

## Overview

A global learning platform operates a simple public-facing web application that users access daily. Currently, the application is deployed in a single AWS Region and relies on one Application Load Balancer (ALB) and a single EC2 instance.

This setup causes several challenges:

- Users in other continents face higher latency
- If the Region goes down, the entire application becomes unavailable
- There is no automatic failover or backup Region
- All traffic depends on one endpoint
- The team cannot direct users to the closest Region for better performance

My job is to design and build a **highly available**, **multi-region** web application using AWS services that support:

- Independent deployments in two AWS Regions
- Health-based routing
- Automatic regional failover
- A single global entry point for users
- A clear way to see which Region is serving traffic

To achieve the above mentioned solution, I have deploy the same lightweight HTML web application in **two AWS Regions**, one primary and one secondary. Each Region will run its own EC2 instance behind an Application Load Balancer. 

Then, using **AWS Global Accelerator**, we will create a single global endpoint that routes users to the nearest healthy AWS Region for better performance.

## About this project

In this hands-on project, I performed the following tasks:

- Deploy a styled web app in two AWS Regions
- Create ALBs to expose the app in each Region
- Add Route 53 Health Checks for continuous monitoring
- Configure AWS Global Accelerator with two endpoint groups
- Test how traffic moves between Regions
- Simulate a failure and observe automatic failover

## AWS services used:

- **AWS Global Accelerator** - Global routing & failover
- **Elastic Load Balancing (ALB)** - Regional traffic distribution
- **Amazon EC2** - Web application hosting
- **Amazon VPC** - Networking, subnets, routing
- **Amazon Route 53 Health Checks** - Regional availability monitoring










## Architectural Diagram

![img alt](https://github.com/VenkataDinakar77/AWS-Multi-Region-Failover-Using-Global-Accelerator/blob/a671ae7dcd8f1651c3d8ac80a798cb8b2ce8ecf2/Multi-Region%20Failover%20Architecture%207.00.45%E2%80%AFPM.png)


## Architecture Insights

In this project, deployed a simple web application in two AWS Regions and route users through AWS Global Accelerator. Each Region contains:

- A VPC with public subnets
- One EC2 instance running the web application
- An Application Load Balancer exposing the app

AWS Global Accelerator is positioned in front of both Regions and routes users to the nearest healthy Regional endpoint. If the primary Region becomes unavailable or unhealthy, traffic is automatically redirected to the secondary Region.

#### High-Level Traffic Flow
- Users access the application through a single Global Accelerator endpoint.
- Global Accelerator evaluates endpoint health and user proximity.
- Traffic is routed to the primary Region when it is healthy.
- During a failure or health-check issue, traffic is automatically shifted to the secondary Region.

This architecture provides global application availability, reduced latency, automatic failover, and improved resilience.

#### Region Selection

- **Primary Region:** us-east-2 (Ohio)
- **Secondary Region:** ap-south-1 (Mumbai)

#### Application

The project uses two static HTML files:

- **Region A Version:** Blue header + “Served from Region A”
- **Region B Version:** Green header + “Served from Region B”

These files are inserted into EC2 instances using user data scripts.

#### Networking summary

Each region consists of:

- 1 VPC
- 2 public subnets (for the ALB + EC2 instance)
- 1 Internet Gateway
- 1 route table
- 1 security group allowing: 80- HTTP & All outbound traffic

The environment is intentionally lightweight to keep the focus on **multi-region routing** rather than large-scale infrastructure.

#### Health monitoring

The project uses Amazon Route 53 health checks to monitor the availability of each Application Load Balancer (ALB) endpoint.

These health checks provide additional visibility into the health of each Region and help validate regional availability during testing. In addition, AWS Global Accelerator performs its own health checks to continuously monitor the configured endpoints and support automatic traffic failover when necessary.

## Conclusion

In this project, built and tested a fully functional multi-region web application using AWS Global Accelerator.

Deployed identical applications across two AWS Regions, exposed each application through an Application Load Balancer (ALB), configured health checks, and connected both environments through a single global endpoint.

Also, conducted a real-world failover test:

Region A handled traffic during normal operation.
When Region A became unhealthy, traffic was automatically redirected to Region B.
After Region A recovered, traffic automatically returned without any manual intervention.

This production-grade architecture helps global applications achieve:

- High availability
- Low latency for users worldwide
- Resilience against Regional failures and outages

Through this project, I have gained practical experience designing, deploying, and testing a multi-region AWS architecture— an essential skill for modern Cloud Engineers.








## Author

- [@LinkedIn](https://www.github.com/octokatherine)
- Email Id: dinakar.kunduru0414@gmail.com




