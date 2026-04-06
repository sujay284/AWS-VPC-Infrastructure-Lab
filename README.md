# AWS VPC Infrastructure Lab: Two-Tier Architecture

## 📋 Project Overview
In this hands-on lab, I designed and implemented a secure, two-tier network architecture on **Amazon Web Services (AWS)**. The project involved creating a custom Virtual Private Cloud (VPC) to host a web application and a backend MySQL database with high availability and strict security controls.



## 🛠️ Technical Stack
* **Cloud Provider:** AWS
* **Networking:** VPC, Public/Private Subnets, Internet Gateway (IGW), Route Tables.
* **Compute:** EC2 (Linux Web Server).
* **Database:** Amazon RDS (MySQL 8.0).
* **Security:** Security Groups (Stateful Firewalls).

---

## 🚀 Detailed Implementation Steps

### 1. Networking Configuration
* **VPC Setup:** Created a custom VPC named `My VPC` with a dedicated CIDR block.
* **Public Subnet:** Configured for the Web Tier to allow external traffic via an **Internet Gateway**.
* **Private Subnets:** Created two private subnets across different **Availability Zones (AZs)** to support the RDS DB Subnet Group:
    * **Private Subnet 1:** `10.0.2.0/24`
    * **Private Subnet 2:** `10.0.3.0/24`

### 2. Traffic Control & Routing
* **Internet Gateway:** Attached an IGW to `My VPC` to enable internet connectivity.
* **Route Tables:** Configured a Public Route Table with a default route (`0.0.0.0/0`) pointing to the IGW, then associated it with the Public Subnet.

### 3. Security Architecture (Tiered Defense)
* **Web Security Group:** Allowed inbound **HTTP (Port 80)** traffic from the internet.
* **Database Security Group:** Created a group named `Database`.
* **Rule Nesting:** Configured the database to only allow inbound **MySQL/Aurora (Port 3306)** traffic originating from the Web Server's Security Group ID. This prevents any direct access to the database from the public internet.

### 4. Managed Database Deployment
* **Amazon RDS:** Launched a **MySQL 8.0.x** instance using the `db.t3.micro` class.
* **Connectivity:** * Associated the RDS instance with `My Subnet Group`.
    * Disabled **Public Access** to ensure the database remains isolated within the private subnets.
    * Named the initial database `mydb`.

---

## 🧠 Key Learning Outcomes
* **High Availability:** Learned why AWS requires subnets in at least two Availability Zones for RDS Subnet Groups.
* **Network Isolation:** Successfully separated the application tier (public) from the data tier (private) to minimize the attack surface.
* **Least Privilege:** Applied security group rules that only allow necessary traffic between specific architecture components.

---

## 📸 Lab Evidence
*(Note: Upload your screenshots to your GitHub repository and link them here)*
* **VPC Dashboard**
* **Security Group Rules**
* **Running RDS Instance**
