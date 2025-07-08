# Cost Estimation and Optimization for AWS Infrastructure

This repository provides guidance and sample calculations for estimating the cost of running an AWS architecture that includes EC2 instances, VPC, subnets, EBS volumes, and related network rules. The scenario considered here involves scaling from 2 EC2 instances during normal operations to 4 instances at peak times. The documentation also covers associated AWS resources such as VPC, subnets, EBS storage, and security group (inbound/outbound) rules.


---

## Architecture Overview

- **EC2 Instances:** 2 instances (baseline), scaling to 4 at peak load.
- **VPC:** One dedicated Virtual Private Cloud.
- **Subnets:** At least 2 (public and private).
- **EBS:** Persistent storage attached to each EC2 instance.
- **Security Groups:** Configured with inbound and outbound rules for secure access.

---

## Assumptions

- **AWS Region:** us-east-1 (N. Virginia)
  ![add service and configure price for ec2](https://github.com/user-attachments/assets/5d2133a3-59fc-4f9d-9a1c-5d7254fa023a)
- **EC2 Instance Type:** t3.medium (2 vCPUs, 4GB RAM)
  ![instance type pricing](https://github.com/user-attachments/assets/c51c78d7-c004-4414-af46-0934c4735337)

- **EBS Volume:** 30GB gp3 per instance
  ![EBS](https://github.com/user-attachments/assets/79743ff2-1a26-4e23-99d0-2921861a1e97)
- **VPC & Subnets:** Default AWS pricing 
- **Usage Pattern:** 2 instances running 24x7; 2 additional instances running 8 hours per day (peak)
- **Data Transfer:** Minimal, as per typical web app traffic
  ![inbound and outbound estimate](https://github.com/user-attachments/assets/04ea4ec5-7171-48a8-a818-dde863d095c2)
  ![hourly charge for ondemand instances](https://github.com/user-attachments/assets/b18c2b03-29d9-4650-8be0-2aa068cebb05)

---

## Resource Breakdown

### 1. EC2 Instances

- **Baseline:** 2 x t3.medium (on-demand)
- **Peak:** Additional 2 x t3.medium for 8 hours/day

### 2. VPC and Subnets

- 1 VPC
- 2 Subnets (1 public, 1 private)

### 3. EBS (Elastic Block Store)

- 30GB gp3 volume per instance
- 4 volumes at peak (120GB total), 2 volumes off-peak (60GB total)

### 4. Security Groups (Inbound/Outbound Rules)

- **Inbound:** Allow SSH (port 22) from admin IP, HTTP/HTTPS (80/443) from anywhere
- **Outbound:** Allow all traffic

---

## Cost Estimation
![detailed estimation](https://github.com/user-attachments/assets/72b6d7fd-4bfb-4941-b587-6c011bf748d4)

### **Estimated Monthly Total (Typical Month):**

https://calculator.aws/#/estimate?id=53bc41766e5ac2383f0e9ae92b771dcf00961ad4
---

## Optimization Tips

- **Use Reserved or Savings Plans** for EC2 if workloads are predictable.
- **Right-size instances:** Use smaller/larger instance types as needed.
- **Automate scaling:** Use Auto Scaling Groups to add/remove instances based on load.
- **Monitor EBS usage:** Delete unused volumes and snapshots.
- **Restrict inbound rules:** Minimize open ports to reduce security risks.
- **Review data transfer:** Minimize cross-region or internet-bound traffic.

---

## References

- [AWS Pricing Calculator](https://calculator.aws.amazon.com/)
- [Amazon EC2 Pricing](https://aws.amazon.com/ec2/pricing/on-demand/)
- [Amazon EBS Pricing](https://aws.amazon.com/ebs/pricing/)
- [VPC Pricing](https://aws.amazon.com/vpc/pricing/)
- [Best Practices for Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html)

---

> *For actual deployments, always use the AWS Pricing Calculator and consult the AWS documentation for the latest pricing and best practices.*
