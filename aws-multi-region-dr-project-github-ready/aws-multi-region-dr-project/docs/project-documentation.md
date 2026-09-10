# AWS Multi-Region Highly Available Web Application with Disaster Recovery

## 1. Project Overview

This project demonstrates the design and implementation of a highly available, scalable, secure, and disaster-resilient web application architecture on AWS.

The architecture is deployed across two AWS regions:

- **Primary Region:** `us-east-1`
- **Secondary / DR Region:** `us-west-2`

The primary region handles normal production traffic, while the secondary region is designed to provide disaster recovery capability in case of a major failure in the primary region.

The architecture focuses on:

- High Availability
- Fault Tolerance
- Scalability
- Disaster Recovery
- Network Security
- Load Balancing
- Database Protection
- Multi-Region Resilience

---

# 2. Architecture Diagram

![AWS Architecture](../images/aws-architecture.png)

---

# 3. High-Level Architecture

The application follows a layered architecture.

```text
User
  |
  v
Route 53
  |
  v
AWS WAF
  |
  v
CloudFront
  |
  v
Application Load Balancer
  |
  v
Web Tier
  |
  v
Application Tier
  |
  v
RDS Database
