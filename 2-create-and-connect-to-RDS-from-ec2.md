# Connecting to an AWS RDS MySQL Database

## Step 1: Create an RDS Database in AWS

1. **Sign in to AWS Console**
   - Go to [AWS Management Console](https://aws.amazon.com/console/)
   - Navigate to **RDS** service.

2. **Create a New RDS Instance**
   - Click on **Create database**.
   - Select **Standard Create**.
   - Choose **MySQL** as the database engine.
   - Select the **Free Tier** or appropriate instance type.
   - Configure settings:
     - **DB instance identifier**: e.g., `database-1`
     - **Master username**: Choose an admin username.
     - **Master password**: Set a secure password.

3. **Network & Security**
   - Choose a VPC or use the default one.
   - Set **Public access** to `Yes` (if connecting remotely).
   - Configure security group:
     - Allow inbound rules for **MySQL/Aurora (3306)** from your IP.

4. **Create the Database**
   - Click **Create Database** and wait for it to be available.

## Step 2: Find the RDS Endpoint

1. Navigate to **RDS Console**.
2. Click on your created database.
3. Copy the **Endpoint** (e.g., `database-1.cn2g4mowubxp.us-east-1.rds.amazonaws.com`).

## Step 3: Install MySQL on EC2 Instance

### **Update System Packages**
```bash
sudo dnf update -y
```

### **Download and Install MySQL 8.0**
```bash
sudo wget https://dev.mysql.com/get/mysql80-community-release-el9-4.noarch.rpm
sudo dnf install mysql80-community-release-el9-4.noarch.rpm -y
sudo dnf install mysql-community-server -y
```

### **Start MySQL Service**
```bash
sudo systemctl start mysqld
sudo systemctl enable mysqld
```

## Step 4: Connect to RDS MySQL from EC2

### **Using MySQL CLI**
```bash
sudo mysql -h database-1.cn2g4mowubxp.us-east-1.rds.amazonaws.com -u admin -padminadmin
```

### **Alternative Connection Attempts**
```bash
sudo mysql -h 98.84.170.66 -u root -pAdmin@123
sudo mysql -h ec2-18-212-3-223.compute-1.amazonaws.com -u root -pAdmin@123
```

If you see an error like:
```
ERROR 1130 (HY000): Host '18.212.3.223' is not allowed to connect to this MySQL server
```
This means your MySQL server is restricting remote connections.

## Step 5: Troubleshooting Connection Issues

### 1. Ensure Security Group Allows Connections
- Go to **EC2 Dashboard > Security Groups**.
- Find the security group attached to your RDS instance.
- Edit inbound rules:
  - **Type**: MySQL/Aurora
  - **Protocol**: TCP
  - **Port**: 3306
  - **Source**: Your IP (`x.x.x.x/32`) or `0.0.0.0/0` (not recommended for production).

### 2. Verify RDS Parameter Group
- Ensure `bind-address` is set to `0.0.0.0` (for remote connections).

### 3. Grant Permissions to Remote Users
```sql
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

## Step 6: Connect to RDS from a Local Machine

### Install MySQL Client (if not installed)
#### **Linux/macOS:**
```bash
sudo apt install mysql-client  # Ubuntu
sudo yum install mysql         # RHEL/CentOS
```

#### **Windows:**
- Install [MySQL Workbench](https://dev.mysql.com/downloads/workbench/).

### Connect using MySQL Workbench or CLI
```bash
mysql -h database-1.cn2g4mowubxp.us-east-1.rds.amazonaws.com -u admin -p
```

## Conclusion
You have successfully set up and connected to an AWS RDS MySQL database. Ensure security groups and user permissions are properly configured for smooth connections.

