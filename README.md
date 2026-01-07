# AWS Migration Simulation

## 📖 Overview
This project simulates a real-world enterprise migration where an application running in an on-premises environment is moved to AWS Cloud. Since actual on-prem hardware is not available, a separate VPC in AWS is used to represent the on-prem environment. The project demonstrates how cloud engineers assess, plan, migrate, modernize, secure, and monitor workloads during a cloud migration.

## 🎯 Objective
To migrate a simple web application from a simulated on-prem environment to AWS, deploy it on EC2, modernize the database using RDS, set up networking and security, and implement monitoring and backups while following a real-world lift-and-shift migration workflow.

---

# 🏗️ Architecture Summary

### **Simulated On-Prem Environment**
- VPC-A (10.0.0.0/16)
- Public Subnet (10.0.1.0/24)
- EC2 instance running Apache web server
- Application files stored locally on the instance

### **AWS Cloud Target Environment**
- VPC-B (192.168.0.0/16)
- Public Subnet (192.168.1.0/24)
- EC2 instance hosting the migrated application
- RDS (MySQL/PostgreSQL)
- S3 bucket for backups and file storage
- CloudWatch for monitoring and alarms
- SNS for notifications

---

# 🔁 Migration Flow
1. Build and host the application in the simulated on-prem VPC  
2. Prepare cloud VPC and networking  
3. Lift-and-shift the application to a cloud EC2 instance  
4. Migrate database to RDS  
5. Configure monitoring and alerts  
6. Set up backups and storage in S3  

---

# 🧩 Step-by-Step Implementation

## 1️⃣ Simulated On-Prem Environment Setup
### Create VPC-A
- Configure CIDR block: 10.0.0.0/16  
- Create public subnet and attach Internet Gateway  
- Add route table entry for outbound traffic  

### Launch On-Prem EC2 Instance
- Install Apache web server  
- Host a basic test application:
  ```bash
  sudo yum install httpd -y
  sudo systemctl enable --now httpd
  echo "On-Prem Version of App" | sudo tee /var/www/html/index.html
  ```

---

## 2️⃣ Cloud Environment Setup
### Create VPC-B
- CIDR block: 192.168.0.0/16  
- Create public subnet  
- Attach Internet Gateway and routes  

### Launch Cloud EC2 Instance
- Install Apache web server  
- Prepare it to receive migrated application files  

### Create RDS Database
- MySQL/PostgreSQL engine  
- Configure security groups to allow access only from Cloud EC2  

---

## 3️⃣ Application Migration (Lift & Shift)
### Compress On-Prem App Files
```bash
sudo zip -r app.zip /var/www/html/
```

### Transfer Files to Cloud EC2
```bash
scp -i key.pem ec2-user@<ONPREM-IP>:/home/ec2-user/app.zip .
scp -i key.pem app.zip ec2-user@<CLOUD-IP>:~
```

### Deploy App on Cloud EC2
```bash
sudo yum install httpd -y
sudo systemctl enable --now httpd
unzip app.zip -d /var/www/html/
echo "Cloud Version of App" | sudo tee /var/www/html/index.html
```

---

## 4️⃣ Database Modernization
- Create RDS instance  
- Update the application's configuration on Cloud EC2 to connect using:  
  - RDS endpoint  
  - Username & password  
  - Port  

This shifts the database from a self-managed instance to a managed AWS service.

---

## 5️⃣ Monitoring & Alerts
- Enable CloudWatch metrics for EC2 and RDS  
- Create alarms for CPU, disk, or status-check failures  
- Use SNS to receive email alerts for system issues  

---

## 6️⃣ Backup & Storage
### Create S3 Bucket
- Store application backup ZIP files  
- Upload logs or documentation  

### Add Lifecycle Rule
- Automatically move older files to cheaper storage classes  

---

# 🛡️ Security Measures Implemented
- Security Groups for EC2 and RDS  
- IAM roles for EC2 to interact with S3  
- Network segmentation via separate VPCs  
- No unrestricted access to sensitive resources  

---

# 📈 Skills Demonstrated
- VPC design and networking  
- EC2 deployment and configuration  
- Lift-and-shift migration workflow  
- RDS setup and database modernization  
- S3 bucket configuration and lifecycle policies  
- Monitoring with CloudWatch  
- Alerting using SNS  
- IAM role and policy configuration  

---

# 📝 Project Outcome
This project successfully demonstrates an end-to-end cloud migration process similar to what cloud engineers and professional services teams perform for real clients. It covers networking, compute, storage, database, security, monitoring, and migration best practices, making it a strong portfolio project for cloud roles.

---

