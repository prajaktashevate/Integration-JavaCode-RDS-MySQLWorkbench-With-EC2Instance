# 🏗️ Setup Guide: RDS ↔ EC2 Integration Project

---

## 🔹 Step 1: Create RDS (MySQL)

1. Go to **AWS Console → RDS → Create Database**.
2. Engine = **MySQL** (or Aurora MySQL).
3. Deployment = **Standard**.
4. Templates = **Free tier** (if testing).
5. Set:

   * DB name = `javacode-rds-project`
   * Master username = `admin`
   * Password = `Admin123456`
6. Connectivity:

   * VPC = same VPC where your EC2 will be launched.
   * Public Access = **No** (best practice, keep private).
   * Security group: create/select one (we’ll edit later).
7. Create database → wait for **Available**.

👉 Note the **RDS endpoint** (example: `javacode-rds-project.cb0y2csmwusj.ap-south-1.rds.amazonaws.com`).

<img width="940" height="432" alt="image" src="https://github.com/user-attachments/assets/78db220d-a637-405a-a31e-728435840a0c" />


## 🔹 Step 2: Create EC2 Instance

1. Go to **EC2 → Launch Instance**.
2. AMI = Amazon Linux 2023 (or Ubuntu 22.04).
3. Instance type = t2.micro (free tier).
4. Key pair = choose/create (for SSH).
5. Network settings:

   * VPC = same as RDS.
   * Subnet = same or peered subnet.
   * Security group = allow:

     * **22 (SSH)** from your IP.
     * **8080 (Tomcat)** or **80 (HTTP)** for web app.
6. Launch instance.

👉 Note the **Public IP** (to access via browser).
<img width="940" height="432" alt="image" src="https://github.com/user-attachments/assets/86c20cd6-4607-47b2-9204-9a3c962831e1" />

---

## 🔹 Step 3: Security Group Configuration

* **RDS Security Group**:

  * Inbound rule → MySQL/Aurora (3306).
  * Source = EC2’s security group (not 0.0.0.0/0 ❌).

* **EC2 Security Group**:

  * Inbound → SSH (22) from your IP.
  * Inbound → HTTP (80) or Tomcat (8080) from anywhere.

---

## 🔹 Step 4: Connect EC2 to RDS

1. SSH into EC2:

   ```bash
   ssh -i mykey.pem ec2-user@13.200.251.169
   ```

2. Install MySQL client (for testing):

   ```bash
   sudo dnf install mariadb105 -y
   ```

   (Ubuntu: `sudo apt-get install -y mysql-client`)

3. Test connection:

   ```bash
   mysql -h javacode-rds-project.cb0y2csmwusj.ap-south-1.rds.amazonaws.com -u admin -p
   ```

   If it connects, ✅ EC2 → RDS network is working.

---

## 🔹 Step 5: Create Database & Table in RDS

Inside MySQL shell:

```sql
Database Creation code:-
create database storage;

Database using code:-
use storage;

Table creation code:-

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    address VARCHAR(200),
    contact VARCHAR(15)
);


Table Data:-

INSERT INTO users (name, address, contact) VALUES
('Alice Johnson', '123 Main St, Springfield', '555-1234'),
('Bob Smith', '456 Oak Ave, Rivertown', '555-5678'),
('Charlie Brown', '789 Pine Rd, Lakeview', '555-9012'),
('Diana Prince', '101 Elm St, Metropolis', '555-3456'),
('Evan Davis', '202 Maple Ave, Hilltown', '555-7890'),
('Fiona Carter', '303 Birch Blvd, Roseville', '555-6543'),
('George Lewis', '404 Cedar Ct, Brooksville', '555-8765'),
('Hannah Adams', '505 Walnut Way, Seaside', '555-4321'),
('Ian Thompson', '606 Spruce St, Greenfield', '555-2468'),
('Julia Roberts', '707 Ash Ave, Fairview', '

```
<img width="940" height="543" alt="image" src="https://github.com/user-attachments/assets/28c582d2-4f91-45e4-99d5-44bceccebb69" />

---

## 🔹 Step 6: Install Java on EC2

```bash
Java installation code:-
 sudo yum install java-17-amazon-corretto-devel -y

MySQL installation code:-
sudo dnf install mariadb105 -y

jdbc driver:-
wget https://github.com/awslabs/aws-mysql-jdbc/releases/download/1.1.15/aws-mysql-jdbc-1.1.15.jar


```

## 🔹 Step 7: Deploy Your App

Compile java file:-
javac -cp .:aws-mysql-jdbc-1.1.15.jar UserDatabaseApp.java


Run java file:
java -cp .:aws-mysql-jdbc-1.1.15.jar UserDatabaseApp

<img width="913" height="873" alt="image" src="https://github.com/user-attachments/assets/43124990-b135-4d7e-a3d3-56ba7123d309" />

<img width="940" height="543" alt="image" src="https://github.com/user-attachments/assets/6e05e2d4-993c-40f5-9b83-7afe58ae7670" />

