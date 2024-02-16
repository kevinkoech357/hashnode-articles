---
title: "Utilizing UFW to Enable a Firewall on Your Server"
seoTitle: "UFW"
seoDescription: "firewall ubuntu server"
datePublished: Fri Feb 16 2024 14:02:19 GMT+0000 (Coordinated Universal Time)
cuid: clsopyi6g000909kzgq0c486q
slug: utilizing-ufw-to-enable-a-firewall-on-your-server
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/tiSE_paTt0A/upload/f908a9bb22547ebabee43cf708057c94.jpeg
tags: ubuntu, firewall, ufw

---

In the realm of server security, the utilization of a firewall is paramount. Uncomplicated Firewall (UFW) is a front-end tool for managing netfilter firewall, which aims to make firewall configuration more accessible for users. This article will guide you through using UFW effectively to enable a firewall on your server.

## **Installing ufw**

To install UFW on your server, use the following command:

```bash
sudo apt update
sudo apt install ufw
```

After installation, verify that installation happened correctly:

```bash
sudo ufw --version
# Example utput
kevinkoech357@kevinkoech357:~$ sudo ufw --version
ufw 0.36.2
Copyright 2008-2023 Canonical Ltd.
```

## **Enabling ufw**

After installation, ensure that the default policy for incoming and outgoing traffic is set to deny by using the commands below:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

These commands set the default policies for incoming connections to deny and outgoing connections to allow, which is a common security practice.

## **Configuring UFW**

### **Enabling Specific Ports**

To allow traffic on specific ports, such as SSH (port 22), HTTP (port 80), HTTPS (port 443), and database ports (e.g., MySQL/MariaDB on port 3306, PostgreSQL on port 5432), use the commands:

```bash
sudo ufw allow   22/tcp
sudo ufw allow   80/tcp
sudo ufw allow   443/tcp
sudo ufw allow   3306/tcp
sudo ufw allow   5432/tcp
```

Replace `3306` and `5432` with the actual ports used by your database if they are different. After running these commands, you can check the status of UFW to ensure the rules have been added:

```bash
sudo ufw status
```

The output should show the rules you've just added:

```bash
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere                   
80/tcp                     ALLOW       Anywhere                   
443/tcp                    ALLOW       Anywhere                   
3306/tcp                   ALLOW       Anywhere                   
5432/tcp                   ALLOW       Anywhere                   
22/tcp (v6)                ALLOW       Anywhere (v6)             
80/tcp (v6)                ALLOW       Anywhere (v6)             
443/tcp (v6)               ALLOW       Anywhere (v6)             
3306/tcp (v6)              ALLOW       Anywhere (v6)             
5432/tcp (v6)              ALLOW       Anywhere (v6)
```

### **Enabling Nginx**

To allow traffic for Nginx, which typically listens on ports 80 and 443 for HTTP and HTTPS traffic, you can use the following commands:

```bash
sudo ufw allow 'Nginx HTTP'
sudo ufw allow 'Nginx HTTPS'
```

These commands use the application profiles defined by UFW for Nginx, which should automatically allow traffic on the correct ports.

After adding the Nginx rules, you can verify the changes by rechecking the ufw status:

```bash
sudo ufw status
```

The output should now include rules for Nginx:

```bash
Status: active

To                         Action      From
--                         ------      ----
Nginx HTTP                  ALLOW       Anywhere                   
Nginx HTTPS                 ALLOW       Anywhere                   
...
```

## **Best Practices and Common Mistakes**

### **Best Practices**

* Regularly review and update your firewall rules.
    
* Enable only necessary ports and applications.
    
* Use strong and secure passwords for applications and services.
    
* Limit the number of open ports to reduce the attack surface.
    
* Keep your system and packages up-to date.
    

### **Common Mistakes to Avoid**

* Allowing traffic on all ports without restriction.
    
* Forgetting to reload the firewall after making changes.
    

## **Viewing the List of Applications**

You can view the list of applications and services that have profiles by running:

```bash
sudo ufw app list
```

This command will display a list of applications with their associated profiles.

## **Reloading and Stopping UFW**

### **Reloading ufw**

After making changes to UFW's configuration, it's essential to reload the firewall to apply the new rules:

```bash
sudo ufw reload
```

### **Stopping UFW**

If necessary, you can stop UFW altogether using the command:

```bash
sudo ufw disable
```

## **Conclusion**

Effectively utilizing UFW is a critical aspect of securing your server. By following best practices, avoiding common mistakes, and understanding how to configure and manage it, you can significantly enhance the security of your server and protect it from unauthorized access and malicious activities. Regularly review your firewall configuration to ensure it aligns with your server's security requirements and always stay updated with the latest security best practices.