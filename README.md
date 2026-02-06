# Securing-and-monitoring-of-EC2
Securing and monitoring of EC2
Below is a **GitHub-ready, professional README.md version** of your lab. It is structured, concise, technically clear, and formatted using proper Markdown conventions.

You can copy and paste this directly into your repository.

---

# 🔐 Introduction to Cloud Security: Securing AWS EC2 Instances

## 📘 Project Overview

This project demonstrates foundational cloud security practices by deploying and hardening an AWS EC2 instance. The lab covers secure configuration of:

* EC2 instance provisioning
* Security groups (network firewall rules)
* SSH key-based authentication
* Linux user and privilege management
* SSH hardening
* Amazon CloudWatch monitoring and alerting

These are essential baseline controls for securing Infrastructure as a Service (IaaS) workloads in AWS.

---

## 🎯 Objectives

By completing this project, you will:

* Launch a secure EC2 instance
* Restrict network access using security groups
* Implement SSH key-based authentication
* Disable root login and password authentication
* Configure least-privilege user access
* Set up monitoring and alerting with CloudWatch

---

## 🧰 Prerequisites

* Basic understanding of cloud computing concepts
* AWS account (Free Tier eligible)
* Familiarity with Linux command line
* Installed tools:

  * AWS Management Console access
  * AWS CLI optional
  * SSH client OpenSSH 

---

# 🚀 Exercise 1: Launch an EC2 Instance

### Steps

1. Log in to the **AWS Management Console**
2. Navigate to **EC2 Dashboard**
3. Click **Launch Instance**
4. Configure:

   * **Name**: Secure-EC2-Lab
   * **AMI**: Amazon Linux 2023 (Kernel 6.1)
   * **Instance Type**: `t3.micro` (Free Tier eligible)
5. Create a **new key pair**

   * Download the `.pem` file securely
6. Select:

   * VPC
   * Public subnet
7. Create a new **Security Group**

   * Allow SSH (Port 22)
   * Source: **Your Public IP only**
8. Leave default settings for:

   * Instance details
   * Storage
9. Review and launch

### ✅ Expected Result

* EC2 instance is running
* Instance is reachable via SSH
* Security group restricts SSH access to your IP only

---

# 🔑 Exercise 2: Connect to the EC2 Instance

From your terminal:

```bash
chmod 400 your-key-pair.pem
ssh -i "your-key-pair.pem" ec2-user@your-instance-public-dns
```

### ✅ Expected Result

* Successful SSH login to EC2 instance
* Authenticated using key-based access

---

# 🛡️ Exercise 3: Harden the EC2 Instance

## 1️⃣ Update the System

```bash
sudo yum update -y
sudo yum upgrade -y
```

## 2️⃣ Create a Non-Root User

```bash
sudo adduser newuser
sudo usermod -aG wheel newuser
```

This grants sudo privileges while avoiding direct root usage.

## 3️⃣ Secure SSH Configuration

Edit SSH configuration:

```bash
sudo vi /etc/ssh/sshd_config
```

Modify the following:

```
PermitRootLogin no
PasswordAuthentication no
```

Restart SSH:

```bash
sudo systemctl restart sshd
```

### 🔐 Security Improvements Implemented

* Disabled root login
* Enforced key-based authentication
* Removed password-based authentication
* Followed principle of least privilege

---


### ✅ Expected Result

* SSH access restricted to trusted IP
* Reduced external attack surface

---

# 📊 Exercise 5: Enable Monitoring with CloudWatch

1. Navigate to **CloudWatch**
2. Select **Alarms → Create Alarm**
3. Choose EC2 Metric:

   * CPUUtilization
4. Configure:

   * Threshold: > 60%
   * Duration: 2 minutes
5. Configure notification (SNS email)
6. Create alarm

### ✅ Expected Result

* Automated alert if CPU exceeds threshold
* Baseline operational monitoring enabled

---

# 🏗️ Security Concepts Demonstrated

* Infrastructure as Code readiness mindset
* Network segmentation via security groups
* Key-based authentication
* Linux privilege management
* Secure SSH configuration
* Monitoring and alerting
* Defense-in-depth principles

---

# 🧠 Key Takeaways

* Never allow unrestricted SSH access (`0.0.0.0/0`)
* Always use key-based authentication
* Disable root login
* Implement least privilege access controls
* Enable monitoring for visibility and incident response
* Regularly update system packages

---

# 📂 Repository Structure (Example)

```
/ec2-cloud-security-lab
│
├── README.md
├── screenshots/
│   ├── ec2-instance.png
│   ├── security-group.png
│   ├── ssh-config.png
│   └── cloudwatch-alarm.png
```

---

# 🏁 Conclusion

This lab demonstrates foundational AWS EC2 hardening techniques aligned with cloud security best practices. These controls significantly reduce attack surface and improve system resilience.

This project reflects real-world baseline security implementation for AWS-hosted workloads.
