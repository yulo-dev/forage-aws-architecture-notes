## [Exercise only] Client Response – AWS Architecture Proposal for Fastier

Hi Lilly,

Thank you so much for reaching out, and congratulations on the growth of Fastier!

Based on the pain points you've described — slow response times under load, memory-related crashes, downtime during deployments, and the lack of a disaster recovery plan — I’ve designed a proposed AWS architecture that focuses on scalability, high availability, and simplicity.


**Overview of the Proposed Architecture:**

The solution centers around Elastic Beanstalk, which simplifies deployment and integrates key components like load balancing, EC2 application servers, and RDS databases. These services can be scaled independently to match demand and reduce costs.

Here’s a high-level summary of the architecture:

- **Elastic Beanstalk** for Flask backend deployment  
- **EC2 Auto Scaling Group** to handle variable traffic  
- **Elastic Load Balancer (ELB)** for request distribution and redundancy  
- **RDS (PostgreSQL)** for a managed, fault-tolerant database  
- **S3** for file and backup storage (and static file hosting, if needed)  
- **Route 53** for DNS and routing management  
- **CodePipeline** for CI/CD and blue/green deployments  
- **Multi-AZ setup (optional)** for improved disaster recovery and uptime

**Component Breakdown & Why They Were Chosen:**

- **Elastic Beanstalk:**
Allows for simplified deployment and scaling. It ties together EC2, RDS, and ELB while offering rolling or blue/green deployments to eliminate downtime.

- **EC2 Auto Scaling Group:**
Automatically increases or decreases instance count based on traffic, solving your memory and performance issues without overpaying during low-load periods.

- **Elastic Load Balancer:**
Distributes incoming requests across healthy EC2 instances in one or more availability zones, improving reliability and response times.

- **RDS (PostgreSQL):**
A fully managed relational database service that supports Multi-AZ replication and backup features, keeping your database resilient and scalable.

- **S3:**
Initially recommended for backup storage (e.g., RDS snapshots), with the option to host static content as your frontend grows.

- **Route 53:**
Manages DNS routing and integrates directly with ELB for seamless traffic management.

- **CodePipeline:**
Enables automated deployments using CI/CD. Supports blue/green deployment workflows so you can deploy new versions without causing downtime.

- **Optional: Multi-AZ Deployment:**
Deploying across multiple availability zones adds redundancy and failover capabilities. While this increases cost slightly, it significantly improves reliability.

**Billing Considerations**

Each AWS service is billed based on usage:

- **EC2 / RDS**: Billed hourly by instance type (e.g., t3.medium)  
- **ELB**: Charges based on uptime and request volume  
- **S3**: Charged by GB stored and data retrieval  
- **CodePipeline**: Charged per active pipeline/month  
- **Route 53**: Minimal charges for DNS queries and hosted zones  

We recommend using the [AWS Pricing Calculator](https://calculator.aws/) to forecast more precise costs after some initial performance testing. Since AWS billing is modular, you only pay for what you use, and can scale down during low-demand periods.


Please let me know if you'd like me to provide an architecture diagram or set up a quick call to walk through the details. Happy to assist!

Best regards,  
Yulo  
Solutions Architect  
Amazon Web Services

---
title: Client Email Simulation – AWS Architecture Proposal

date: July 2025
