# Task 1: Designing a Simple, Scalable, Hosting Architecture (AWS)

## 1. Overview

This task explores how to design a scalable hosting architecture using AWS.  
We can understand key AWS services — especially compute, storage, deployment, and load distribution tools — to make cost-effective and reliable decisions.

---

## 2. Key AWS Services

### General Services

| Service | Purpose | Billing Summary |
|--------|---------|----------------|
| **CodePipeline** | CI/CD pipeline; automates code build and deployment | Charged per pipeline |
| **Elastic Load Balancing (ELB)** | Distributes traffic across compute resources (EC2, Lambda, Fargate) with health checks | Billed based on uptime and traffic |
| **RDS** | Managed relational database (e.g., MySQL, PostgreSQL) | Charged like EC2 (based on instance specs and uptime) |
| **Route 53** | DNS and domain name service | Usage-based pricing |
| **S3** | Cloud object storage (e.g., images, logs, static files) | Charges for storage size, storage class, and retrieval activity |

---

### Application Executors

| Service | Description | Billing & Notes |
|---------|-------------|-----------------|
| **EC2** | Scalable virtual machines | Charged hourly by specs (CPU, RAM); must restart to resize |
| **Fargate** | Run Docker containers without managing servers | Pay by resources (CPU, RAM) and runtime |
| **Lambda** | Serverless function execution (event-driven) | Pay by memory used, execution time, and request count |
| **Lightsail** | Simplified EC2 (easier setup, fewer configs) | Fixed-rate pricing; must clone instance to change resources |
| **Elastic Beanstalk** | Automates app deployment using EC2 + RDS + ELB | Billed based on the underlying resources (EC2, RDS, ELB); supports auto-scaling and rolling deployments |

---

## 3. Availability Zones (AZ)

- Use multiple AZs for **fault tolerance**
- Cost scales with the number of zones your services span
- Helps ensure uptime during infrastructure failure

---

## 4. Why Choose Elastic Beanstalk?

Elastic Beanstalk is a great choice for **simplified deployment and auto-scaling**, because it bundles:

- **EC2**: For running the application servers
- **RDS**: For managing relational databases
- **Elastic Load Balancer (ELB)**: For routing traffic to healthy instances
- **Auto Scaling**: To scale EC2 instances up/down as needed
- **CodePipeline Integration**: Supports blue/green deployment via CodePipeline
- **Multi-language support**: Python, Node.js, Java, Go, etc.

---

## 5. Cost Considerations

- Each AWS service has its own pricing model based on usage
- Pricing varies by region, but **billing model is consistent**:
  - **EC2, RDS, ELB**: Charged hourly by resource
  - **S3**: Charged by GB stored + retrievals
  - **Lambda**: Charged by execution count + duration
- Use the [AWS Pricing Calculator](https://calculator.aws/) for region-specific estimates.

---

## 6. Exercise: Suggested AWS Stack

Based on the service features and billing models described above, here’s a simple AWS architecture that would work well for hosting a web application.

The goal is to support:
- Basic backend and database functionality
- Easy auto-scaling as traffic increases
- Simple, low-maintenance deployment
- Reasonable high availability (e.g. across availability zones)

I chose Elastic Beanstalk as the core platform because it ties together EC2, RDS, and ELB, and handles most of the deployment and scaling automatically. It’s a good fit for small to medium-scale apps without needing to manually configure a lot of individual services.

Here’s how each part of the stack maps to specific AWS services:

| Component | Service |
|----------|---------|
| **App Hosting** | Elastic Beanstalk (with EC2) |
| **Database** | RDS (MySQL/PostgreSQL) |
| **DNS** | Route 53 |
| **Load Balancing** | Elastic Load Balancing |
| **CI/CD** | CodePipeline |
| **Static Assets** | S3 |
| **High Availability** | Deploy across multiple AZs |
