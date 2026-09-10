# AWS Multi-Region Highly Available Web Application with Disaster Recovery

## 📌 Project Overview

This project demonstrates the design and implementation of a **highly available, scalable, secure, and disaster-resilient web application architecture on AWS**.

The architecture uses **two AWS regions**:

- **Primary Region:** `us-east-1`
- **Secondary / DR Region:** `us-west-2`

The primary region handles production traffic, while the secondary region is maintained as a **warm standby environment** for disaster recovery.

The architecture is designed to provide:

- High Availability
- Fault Tolerance
- Auto Scaling
- Disaster Recovery
- Network Security
- Load Balancing
- Database Protection
- Multi-Region Resilience

---

## 🏗️ Architecture Diagram

![AWS Architecture](./images/aws-architecture.png)

---

## 🔄 High-Level Traffic Flow

The application request follows this flow:

```text
User
  ↓
Route 53
  ↓
AWS WAF
  ↓
CloudFront
  ↓
Application Load Balancer (ALB)
  ↓
Web Tier
  ↓
Application Tier
  ↓
RDS Database
