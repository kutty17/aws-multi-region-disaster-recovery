# Project Documentation

## Project Overview

This project implements a highly available, multi-tier AWS web application architecture with a warm-standby disaster recovery (DR) environment.

The primary production environment runs in **AWS us-east-1**, while **us-west-2** is maintained as a **warm standby** for disaster recovery.

The architecture is designed to provide:

- High availability across multiple Availability Zones
- Web and application tier auto scaling
- Load balancing for web and application traffic
- Database redundancy and cross-region replication
- Cross-region backup and restore
- DNS-based traffic management
- Web application protection using AWS WAF
- CDN-based content delivery using Amazon CloudFront

## Architecture

![AWS Architecture](./images/aws-architecture.png)

### Traffic Flow

Client
→ Amazon Route 53
→ AWS WAF
→ Amazon CloudFront
→ Elastic Load Balancer
→ Web Tier
→ Application Tier
→ Amazon RDS

### Primary Region

**us-east-1 (Active / Production)**

- VPC
- Two Availability Zones
- Public subnets
- Web subnets
- Application subnets
- Database subnets
- NAT Gateways
- Bastion host
- Web-tier EC2 instances
- Application-tier EC2 instances
- Auto Scaling Groups
- Elastic Load Balancers
- Amazon RDS
- AWS Backup

### Disaster Recovery Region

**us-west-2 (Warm Standby)**

A similar application stack is maintained in the secondary region so that services can be restored or promoted during a regional failure.

## AWS Services Used

| Service | Purpose |
|---|---|
| Amazon Route 53 | DNS and traffic routing |
| AWS WAF | Web application firewall |
| Amazon CloudFront | CDN and edge delivery |
| Amazon VPC | Network isolation |
| EC2 | Web, application, and bastion servers |
| Elastic Load Balancing | Distributes traffic across instances |
| Auto Scaling | Maintains desired EC2 capacity |
| NAT Gateway | Outbound internet access from private tiers |
| Amazon RDS | Relational database |
| AWS Backup | Backup and cross-region recovery |
| Availability Zones | Fault isolation within a region |

## Network Design

Each region contains a VPC distributed across two Availability Zones.

Each Availability Zone contains:

1. Public subnet
2. Web subnet
3. Application subnet
4. Database subnet

The public subnet contains the NAT Gateway and bastion host. Web and application workloads are placed in their respective private subnets, while RDS instances are placed in the database subnet group.

## High Availability

High availability is achieved through:

- Multiple Availability Zones
- Load balancers
- EC2 Auto Scaling Groups
- Redundant web and application instances
- Multi-AZ database design
- Independent NAT Gateways per AZ where applicable

If an EC2 instance fails, Auto Scaling can replace it. If one Availability Zone becomes unavailable, traffic can be directed to healthy resources in the other AZ.

## Disaster Recovery

The DR strategy uses a **warm-standby** model.

The secondary region contains the required infrastructure so that the application can be recovered quickly if the primary region becomes unavailable.

### Cross-Region Protection

- AWS Backup copies backups to the secondary region.
- Backup Vaults are maintained for recovery.
- Database replication/read-replica mechanisms provide cross-region database protection.
- The secondary environment can be restored/promoted during a disaster.

## Security Considerations

Recommended security controls include:

- Security Groups with least-privilege inbound rules
- Private subnets for application and database workloads
- AWS WAF in front of the application
- IAM roles instead of hard-coded AWS credentials
- Encryption for databases and backups
- Restricted administrative access to the bastion host
- CloudFront and HTTPS for secure client communication

## Scaling

The web and application tiers use Auto Scaling Groups.

Example behavior:

- Increased CPU/request load → Auto Scaling launches additional EC2 instances.
- Reduced load → Auto Scaling can terminate unnecessary instances.
- Load Balancers distribute traffic across healthy instances.

## Failure Scenarios

### EC2 Instance Failure

Auto Scaling detects the unhealthy instance and launches a replacement.

### Availability Zone Failure

The load balancer routes traffic to healthy resources in the remaining Availability Zone.

### Database Failure

The configured RDS redundancy/replication strategy provides database recovery or failover.

### Primary Region Failure

Route 53/DR procedures can redirect users toward the warm-standby environment in **us-west-2**, with database and backup recovery procedures used as required.

## Project Outcome

This project demonstrates a production-style AWS architecture that combines:

**High Availability + Scalability + Security + Backup + Cross-Region Disaster Recovery**

It is suitable as a cloud/DevOps portfolio project to demonstrate practical knowledge of AWS networking, compute, load balancing, auto scaling, databases, DNS, security, and disaster recovery.

## Repository Structure

```text
aws-multi-region-dr-project/
├── README.md
├── .gitignore
├── docs/
│   └── project-documentation.md
└── images/
    └── aws-architecture.png
```

## Author

**Dineshkumar**

Cloud / AWS Project
