
---

# 2. `docs/project-documentation.md`

Now use this as your **detailed technical documentation**:

```markdown
# AWS Multi-Region Highly Available Web Application
# Detailed Project Documentation

## 1. Introduction

This document describes the design and implementation of a highly available, multi-tier web application architecture on AWS.

The architecture is designed with two major objectives:

1. Maintain application availability during infrastructure failures.
2. Provide disaster recovery capability in the event of a regional failure.

The primary production environment is hosted in **us-east-1**, while **us-west-2** is used as a warm standby Disaster Recovery environment.

---

# 2. Project Objectives

The main objectives of this project are:

- Design a highly available AWS architecture
- Deploy resources across multiple Availability Zones
- Separate application components into different network tiers
- Implement load balancing
- Implement EC2 Auto Scaling
- Protect the application using AWS WAF
- Use CloudFront for content delivery
- Implement a highly available database architecture
- Implement cross-region backup/recovery
- Design a warm standby DR environment
- Understand failure scenarios and recovery procedures

---

# 3. Overall Architecture

![AWS Architecture](../images/aws-architecture.png)

The architecture consists of:

```text
Users
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
Amazon RDS
