# Project : Setting Up ALB with AWS WAF to block SQL Injection, Geo Location and Query string ✅
<img width="1056" height="515" alt="pro" src="https://github.com/user-attachments/assets/e1c03760-c9a7-4591-93dc-2fccaea7ddc6" />

---

## Overview

- [ ] This project introduces the use of an **Application Load Balancer** to distribute traffic across two EC2 instances with advanced security features using **AWS WAF**.
- [ ] Learn to deploy **AWS WAF Web ACL** to customize security rules, blocking specific requests based on location, SQL injections, and query strings.
- [ ] Configure two **EC2 instances** to simulate a real-world scalable and secure architecture.
- [ ] Understand the interaction of **AWS WAF** with **Elastic Load Balancing** to protect applications against common web exploits.
- [ ] AWS WAF controls traffic by allowing only legitimate requests based on custom rules, offering a **pay-as-you-go pricing model**.

---

## 🔗 Task 1: Sign in to AWS Management Console

- [ ] Click on **Open Console** to redirect to AWS Console.
- [ ] Sign in and set the default region to **US East (N. Virginia) `us-east-1`**.

---

## 🔗 Task 2: Launch First EC2 Instance

- [ ] Go to **EC2** under **Services**.
- [ ] Click on **Launch Instance**.
- [ ] Configure:
      -  Name: **WAF-server1**
      - AMI: **Ubuntu**
      - Instance Type: **t2.micro**
      - Key Pair: **WAF-serverKey (.pem or .ppk)**
      
<img width="1667" height="262" alt="ec2" src="https://github.com/user-attachments/assets/8fe259ba-f068-40dc-a28b-453b8771a0f5" />


- [ ] Network Settings:
      Set Auto-assign public IP to Enable.
      Create Security Group MyWAF-serverSG with rules:
      SSH from Anywhere
      HTTP from Anywhere
      HTTPS from Anywhere
- [] User data:
```bash
#!/bin/bash
sudo su
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
echo "<html><h1> Welcome to Mylabs Server 1 </h1></html>" >> /var/www/html/index.html

```
- [ ]   Click Launch instance and wait for it to start.


## 🔗Task 3: Launch Second EC2 Instance
- [ ] Click on **Launch Instances.**
- [ ] Configure:
    -  Name: **WAF-server2**
    - AMI: **Ubuntu**
    - Instance Type: **t2.micro**
    - Key Pair: **WAF-serverKey (.pem or .ppk)**
- [ ] Network Settings:
  - Set Auto-assign Public IP to Enable.
  - Use existing Security Group **MyWAF-serverSG.**
User Data:
```bash
#!/bin/bash
sudo su
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
echo "<html><h1>Welcome to Mylabs Server 2</h1></html>" >> /var/www/html/index.html
```
Click Launch Instance and wait for it to start.


# Task 4: Create a Target Group

- [ ] Go to **Target Groups** under **Load Balancing** in EC2 console.
- [ ] Click **Create target group**.
- [ ] Configure:
  - Target type: **Instances**
  - Name: `MyWATargetGroup`
  - Protocol: **HTTP**
  - Port: **80**
- [ ] Health Checks:
  - Protocol: **HTTP**
- [ ] Register **WAF-server1** and **WAF-server2** as targets.
- [ ] Click **Create target group**.


## 🔗 Task 5: Create an Application Load Balancer
- [ ] Go to Load Balancers under Load Balancing in EC2 console.
- [ ] Click Create Load Balancer.
- [ ] Select Application Load Balancer and configure:
   Name: **MyWAFLoadBalancer**
   Scheme: Internet-facing
   IP address type: IPv4
- [ ] Network Mapping:
     VPC: Default
     Mappings: All Availability Zones
- [ ] Security Group: Use **MyWAF-serverSG.**
- [ ] Listeners and Routing:
  - Protocol: HTTP
  - Port: 80
- [ ] Default action: Forward to **MyWAFTargetGroup**
- [ ] Click Create load balancer.

## 🔗 Task 6: Test Load Balancer DNS
- [ ] Verify targets are Healthy under **MyWAFTargetGroup.**
- [ ] Go to Load Balancers and note down the DNS name of **MyWAFLoadBalancer.**
- [ ] Enter the DNS in a browser to see the index.html page.
- [ ] Test with SQL Injection and Query String:
       Example SQL Injection: http://<ELB DNS>/product?item=securitynumber'+OR+1=1--
       Example Query String: http://<ELB DNS>/?admin=123456

## 🔗 Task 7: Create AWS WAF Web ACL
- [ ] Go to WAF & Shield under Security, Identity & Compliance.
- [ ] Click Create Web ACL.
- [ ] Configure:
       Name: **MyWAFWebAcl**
       Description: WAF for SQL Injection, Geo location and Query String parameters
       Resource type: Regional resources
       Region: US East (N. Virginia)
- [ ] Add managed rule groups:
       GeoLocationRestriction
       QueryStringRestriction
       AWS SQL Database
- [ ] Set Default action to Allow.
- [ ] Review and Create web ACL.

## 🔗 Task 8: Test Load Balancer DNS
- [ ] Test the load balancer again to ensure WAF rules are blocking SQL Injection and unauthorized Query Strings.

✅ Successfully configured Application Load Balancer with AWS WAF! 🎉

<img width="775" height="321" alt="web page" src="https://github.com/user-attachments/assets/a871dd7a-9a0d-4adf-89e8-014bd491ae8d" />

