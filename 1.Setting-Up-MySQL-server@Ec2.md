**Setting Up MySQL 8.0 on an Amazon EC2 Instance**

## **Introduction**
This document provides step-by-step instructions for installing and setting up MySQL 8.0 on an Amazon EC2 instance running a Linux-based distribution (Amazon Linux or CentOS-based systems).

---

## **Prerequisites**
- An Amazon EC2 instance with a Linux-based operating system.
- `sudo` privileges on the instance.
- Internet access to download the MySQL repository.

---

## **Step 1: Update the System Packages**
Run the following command to update all system packages:
```bash
sudo dnf update -y
```

---

## **Step 2: Download and Install MySQL Repository**
Download the MySQL Yum repository package:
```bash
sudo wget https://dev.mysql.com/get/mysql80-community-release-el9-4.noarch.rpm
```

Install the MySQL Yum repository package:
```bash
sudo dnf install mysql80-community-release-el9-4.noarch.rpm -y
```

---

## **Step 3: Install MySQL Server**
Run the following command to install MySQL 8.0:
```bash
sudo dnf install mysql-community-server -y
```

Check if MySQL is installed successfully:
```bash
mysql -V
```

---

## **Step 4: Start and Enable MySQL Service**
Start the MySQL service:
```bash
sudo systemctl start mysqld
```

Enable MySQL to start automatically on boot:
```bash
sudo systemctl enable mysqld
```

---

## **Step 5: Retrieve the Default Root Password**
MySQL generates a temporary root password during installation. Retrieve it using:
```bash
sudo cat /var/log/mysqld.log | grep 'password'
```

Copy this password, as it will be required for the initial login.

---

## **Step 6: Log In to MySQL**
Use the following command to log in as the root user:
```bash
sudo mysql -u root -p
```

Enter the temporary root password obtained in the previous step.

---

## **Step 7: Change the Root Password (Optional but Recommended)**
Once logged in, change the root password for security reasons:
```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'YourNewStrongPassword';
```
Replace `YourNewStrongPassword` with a strong password of your choice.

---

## **Step 8: Verify MySQL Status**
Check if MySQL is running properly:
```bash
sudo systemctl status mysqld
```

---

## **Step 9: View Command History (Optional)**
To view previously executed commands in the terminal:
```bash
history
```

---

## **Conclusion**
You have successfully installed and configured MySQL 8.0 on your Amazon EC2 instance. You can now create databases, manage users, and configure MySQL settings based on your application requirements.

For further configuration and security best practices, refer to the [official MySQL documentation](https://dev.mysql.com/doc/).

