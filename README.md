<img width="1917" height="1078" alt="Screenshot 2026-11-27 120745" src="https://github.com/user-attachments/assets/77f88f0c-4db7-403b-9dcc-34515d49d02c" /><img width="1917" height="1078" alt="Screenshot 2026-11-27 120554" src="https://github.com/user-attachments/assets/afe9fb1f-63e0-4c0a-8483-15e136d9a00b" /># ☁️ Fortune Cloud – PHP Signup Form with MariaDB on AWS

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

![Fortune Cloud Signup Form](![Uploading Screenshot 2026-11-27 120554.png…]
)

### Registration Success Page

![Registration Success](<img width="1917" height="1078" alt="Screenshot 2026-11-27 120629" src="https://github.com/user-attachments/assets/fdaa8b82-e817-449d-9570-d6762f7c9395" 
)

### MariaDB Database Verification

![Database Verification](Screenshot 2026-11-27 120745.png)

*Add your actual screenshots to the `screenshots/` folder.*

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

`
