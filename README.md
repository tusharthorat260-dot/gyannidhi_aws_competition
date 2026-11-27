# Task-1

# ☁️ Fortune Cloud – PHP Signup Form with MariaDB on AWS

A modern and responsive **User Registration System** built using HTML, CSS, PHP, and MariaDB, deployed on an AWS EC2 Linux instance using Apache Web Server.

This project allows users to create an account by submitting their personal details through a modern signup form. PHP validates the submitted information, securely hashes the password, and stores the registration data in a MariaDB database.

## 🚀 Project Overview

The Fortune Cloud Signup System demonstrates how to build and deploy a basic web application on AWS EC2.

**Key Features:**

* Modern and responsive signup form UI
* User registration with Full Name, Email, and Phone Number
* Password and Confirm Password validation
* Terms & Privacy Policy acceptance
* Server-side PHP validation
* Secure password hashing using `password_hash()`
* Prepared SQL statements to prevent SQL injection
* MariaDB database integration
* Duplicate email prevention
* Registration success and error messages

## 🛠️ Technology Stack

| Technology           | Purpose              |
| -------------------- | -------------------- |
| AWS EC2              | Cloud hosting        |
| Linux (Amazon Linux) | Operating system     |
| Apache (HTTPD)       | Web server           |
| PHP                  | Backend development  |
| MariaDB              | Database management  |
| HTML5                | Web page structure   |
| CSS3                 | Responsive UI design |
| Git & GitHub         | Version control      |

## 🏗️ Architecture Diagram

```mermaid
flowchart LR
    U[User / Browser] -->|HTTP Request| EC2

    subgraph AWS["AWS Cloud"]
        subgraph SERVER["EC2 Linux Instance"]
            A[Apache Web Server]
            P[PHP Backend]
            D[(MariaDB Database)]
            A --> P
            P -->|Prepared INSERT Query| D
        end
    end

    EC2 --> A
    P -->|Success / Error Response| U
```

## 📋 Signup Form Fields

The registration form collects the following information:

| Field              | Description             |
| ------------------ | ----------------------- |
| Full Name          | User's full name        |
| Email Address      | Valid email address     |
| Phone Number       | Contact number          |
| Password           | Minimum 8 characters    |
| Confirm Password   | Password confirmation   |
| Terms & Conditions | User agreement checkbox |

## 📸 Project Screenshots

### Signup Form

![Fortune Cloud Signup Form](https://github.com/tusharthorat260-dot/gyannidhi_aws_competition/blob/38eb00a2eead5ef08c373748df3f3cbfe7cddbef/Screenshot%202026-11-27%20120629.png)
### Registration Success Page

![Registration Success](https://github.com/tusharthorat260-dot/gyannidhi_aws_competition/blob/acca647ed21f0c819929a0c6e16447d975075baf/Screenshot%202026-11-27%20120554.png)

### MariaDB Database Verification

![Database Verification](https://github.com/tusharthorat260-dot/gyannidhi_aws_competition/blob/dbcc78a208ea57311f60bd48e52999b777ca00fb/Screenshot%202026-11-27%20120745.png)


## 🗄️ Database Configuration

**Database Name:** `FCT`

**Table Name:** `user`

### Create Database

```sql
CREATE DATABASE FCT;

USE FCT;
```

### Create User Table

```sql
CREATE TABLE user (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    phone VARCHAR(20) NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 📂 Project Structure

```text
fortune-cloud-signup/
│
├── index.html
├── submit.php
├── screenshots/
│   ├── signup-form.png
│   ├── success-page.png
│   └── database.png
│
└── README.md
```

## ⚙️ AWS EC2 Deployment

### Step 1: Launch EC2 Instance

* Login to AWS Management Console.
* Launch an Amazon Linux EC2 instance.
* Configure Security Group.
* Allow HTTP (Port 80) access.
* Connect to EC2 using SSH.

### Step 2: Install Required Packages

```bash
sudo yum update -y

sudo yum install -y httpd php php-mysqlnd mariadb-server
```

### Step 3: Start Services

```bash
sudo systemctl enable --now httpd

sudo systemctl enable --now mariadb
```

### Step 4: Configure MariaDB

```bash
sudo mysql
```

Execute:

```sql
CREATE DATABASE FCT;

USE FCT;

CREATE TABLE user (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) NOT NULL UNIQUE,
    phone VARCHAR(20) NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Step 5: Deploy Project Files

Copy your project files into Apache web root:

```bash
sudo mkdir -p /var/www/html/fortune-cloud

sudo cp index.html submit.php /var/www/html/fortune-cloud/
```

### Step 6: Restart Apache

```bash
sudo systemctl restart httpd
```

### Step 7: Access Website

Open your browser:

```text
http://YOUR-EC2-PUBLIC-IP/fortune-cloud/
```

Your Fortune Cloud signup page should now be accessible.

## 🔐 Security Implementation

* Passwords are stored using PHP `password_hash()`.
* SQL queries use prepared statements.
* Email addresses are validated using PHP.
* Password confirmation is checked before insertion.
* HTML output is escaped using `htmlspecialchars()`.
* Database credentials should be stored securely and not committed to GitHub.
* MariaDB port 3306 should not be exposed publicly.

## 🧪 Database Verification

To verify registered users:

```sql
USE FCT;

DESC user;

SELECT id, name, email, phone, created_at
FROM user;
```

Passwords are stored as hashes and are not displayed in the verification query.

## 📤 GitHub Deployment

Initialize Git:

```bash
git init

git add .

git commit -m "Initial Fortune Cloud signup project"

git branch -M main

git remote add origin YOUR-GITHUB-REPOSITORY-URL

git push -u origin main
```

## 🎯 Learning Outcomes

Through this project, I gained practical experience in:

* Deploying applications on AWS EC2.
* Configuring Apache Web Server.
* Installing and configuring PHP.
* Managing MariaDB databases.
* Connecting PHP applications with MariaDB.
* Implementing secure user registration.
* Using prepared statements and password hashing.
* Managing source code using Git and GitHub.

## 🔮 Future Improvements

* Implement user login and logout functionality.
* Add email OTP verification.
* Add password reset functionality.
* Implement HTTPS using SSL/TLS certificates.
* Move database to AWS RDS.
* Configure CI/CD using GitHub Actions.
* Add AWS CloudWatch monitoring.
* Deploy using a custom domain name.


**Project:** Fortune Cloud – User Registration System

---

# Task-2


# Task-3

# AWS High Availability Web Application with Application Load Balancer


## Project Overview

This project demonstrates how to host a web application on AWS and make it accessible through an **internet-facing Application Load Balancer (ALB)**. The ALB uses two HTTP listeners to route requests to separate target groups:

- **HTTP :80** → `app-tg` → Welcome website
- **HTTP :8080** → `test-app-tg` → CPU monitoring and load-testing dashboard

The VPC console screenshot shows a VPC with four subnets across two Availability Zones, two route tables, an Internet Gateway connection, and a NAT Gateway connection. The ALB console screenshot shows the load balancer active, both listeners configured, and the registered EC2 target reported as healthy in each target group.

## Project Objectives

1. Build a logically segmented AWS network using a VPC and multiple subnets.
2. Publish web applications through an internet-facing Application Load Balancer.
3. Configure listener-to-target-group routing for two application ports.
4. Verify target health and test the application through the ALB DNS name.
5. Demonstrate a CPU monitoring page and generate test CPU load.

## Architecture Diagram

<img width="1536" height="1024" alt="WhatsApp Image 2026-11-27 at 4 19 17 PM" src="https://github.com/user-attachments/assets/9bb7a056-8c45-4075-96de-645c77c61103" />


## AWS Services and Components

| Component | Purpose |
|---|---|
| Amazon VPC | Isolated virtual network for project resources |
| Public subnets | Network subnets intended for internet-facing resources |
| Private subnets | Network subnets intended for internal resources |
| Internet Gateway (IGW) | Provides internet connectivity for resources with suitable public routing |
| NAT Gateway | Allows private-subnet resources to initiate outbound internet access |
| Application Load Balancer | Receives HTTP requests and forwards them to target groups |
| ALB Listener :80 | Routes requests to `app-tg` |
| ALB Listener :8080 | Routes requests to `test-app-tg` |
| EC2 | Hosts the registered application target |
| Target Groups | Define the destinations for listener forwarding and health checks |

## Request Flow

### 1. Welcome Website – Port 80

1. A user opens the ALB DNS name in a browser.
2. The request reaches the ALB on HTTP port `80`.
3. The listener forwards the request to `app-tg`.
4. The target group sends the request to the registered EC2 target.
5. The Fortune Cloud Technologies welcome page is returned to the browser.

**Test URL:**

```text
http://<ALB-DNS-NAME>/
```

### 2. CPU Monitoring Dashboard – Port 8080

1. A user opens the ALB DNS name with port `8080`.
2. The request reaches the ALB listener on port `8080`.
3. The listener forwards the request to `test-app-tg`.
4. The target group sends the request to the registered EC2 target.
5. The CPU dashboard displays CPU usage and provides controls to increase or cancel CPU load.

**Test URL:**

```text
http://application-alb-724886124.us-east-1.elb.amazonaws.com:8080/
```

Replace `<application-alb-724886124.us-east-1.elb.amazonaws.com>` with the DNS name shown in the EC2 → Load Balancers console.

## Implementation Summary

### Network

- Created a VPC named `my-vpc-1`.
- Configured four subnets across two Availability Zones, as shown in the VPC resource map.
- Configured two route tables.
- Connected the network to an Internet Gateway and a NAT Gateway.

### Application Load Balancer

- Created an internet-facing Application Load Balancer named `application-alb`.
- Configured HTTP listeners on ports `80` and `8080`.
- Configured listener forwarding to two target groups:
  - `app-tg`
  - `test-app-tg`

### Target Health

The ALB resource map screenshot shows one registered EC2 target in each target group, and both targets are displayed as **Healthy**. The same EC2 instance ID is visible in both target groups.

## Project Screenshots

### 1. VPC Network Resource Map

Shows the VPC, four subnets, two route tables, and network connections.

<img width="1917" height="1078" alt="Screenshot 2026-11-27 113754" src="https://github.com/user-attachments/assets/ccad28e1-6443-4d07-b4af-c43678a40f24" />


### 2. Application Load Balancer Configuration

Shows the active ALB, HTTP listeners on ports 80 and 8080, both target groups, and healthy registered targets.

<img width="1917" height="1078" alt="Screenshot 2026-11-27 113550" src="https://github.com/user-attachments/assets/a9246d80-56eb-46f4-a914-702c4462a822" />

### 3. CPU Monitoring and Load Testing Dashboard

Shows the CPU usage dashboard with **Increase CPU Load** and **Cancel Load** controls.

<img width="1917" height="1078" alt="Screenshot 2026-11-27 113446" src="https://github.com/user-attachments/assets/e25c8372-1c92-4f32-b4de-13d39b2562a3" />

### 4. Welcome Website

Shows the deployed Fortune Cloud Technologies project welcome page.

<img width="1917" height="1078" alt="Screenshot 2026-11-27 113343" src="https://github.com/user-attachments/assets/633b5d7d-9243-424e-a208-46965b7c20fc" />

## Testing and Validation

| Test | Expected / observed result |
|---|---|
| Open ALB DNS on port 80 | Welcome website is displayed |
| Open ALB DNS on port 8080 | CPU monitoring dashboard is displayed |
| Check ALB state | Active |
| Check `app-tg` target health | Healthy in screenshot |
| Check `test-app-tg` target health | Healthy in screenshot |
| Use CPU load control | Dashboard provides increase/cancel controls |

## Security Recommendations

- Allow inbound HTTP traffic to the ALB only on the required listener ports (`80` and `8080`) for this demonstration.
- Allow the application target's inbound traffic only from the ALB security group, using the actual application ports.
- Do not expose SSH (`22`) to the entire internet; restrict it to a trusted IP or use AWS Systems Manager Session Manager.
- For a production deployment, use HTTPS with an ACM certificate and an HTTPS listener.
- Avoid storing database passwords, access keys, or other secrets in source code or this README.

## Improvements for a Production-Ready Version

- Deploy application instances across multiple Availability Zones.
- Attach an Auto Scaling Group to the appropriate target group(s).
- Add HTTPS using AWS Certificate Manager.
- Configure CloudWatch alarms for CPU utilization, ALB errors, and unhealthy targets.
- Use Route 53 for a custom domain.
- Store application logs centrally and apply least-privilege IAM roles.

## Challenges and Learning Outcomes

- Practiced VPC networking concepts, including subnets, route tables, IGW, and NAT Gateway.
- Learned how ALB listeners forward traffic to target groups.
- Configured separate application access paths using ports `80` and `8080`.
- Validated target health through the ALB console.
- Tested a live welcome page and a CPU monitoring/load-testing dashboard through the ALB DNS name.

## Conclusion

This project demonstrates an AWS-hosted web application accessed through an internet-facing Application Load Balancer. Separate listeners and target groups provide two application endpoints through one load balancer, while the VPC network is organized across multiple subnets and Availability Zones.

The project provided practical experience with AWS networking, load balancing, EC2 target registration, health checks, and application testing.

---

**Project:** AWS Application Load Balancer Web Hosting  
**Organization:** Fortune Cloud Technologies


**Author:** Tushar Thorat


