# Ansible Dynamic Inventory and Database Installation on AWS EC2
This document explains how to **set up Ansible Dynamic Inventory from scratch** using AWS EC2 and **install a database (MySQL)** on EC2 instances discovered dynamically.

---
## Document Details
|     Author      |  Created on  | Version |  Pre Reviewer  | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|-----------------|--------------|---------|----------------|-------------|-------------|-------------|
| Suraj Tripathi  |  2026-01-16  |  1.0    |                |             |             |             |

---
## Table of Contents

1. Introduction  
2. Prerequisites  
3. Ansible Installation  
4. AWS Credentials Configuration  
5. Dynamic Inventory Setup  
6. Testing Dynamic Inventory  
7. Database Installation Using Dynamic Inventory  
8. Verification  
9. Best Practices  
10. Conclusion
11. Contact Details

---
## 1. Introduction

Dynamic Inventory allows Ansible to **automatically discover EC2 instances** from AWS instead of manually defining IP addresses.  
This approach is ideal for **cloud and auto-scaling environments** where servers change frequently.
In this guide, we:
- Configure AWS EC2 Dynamic Inventory
- Discover EC2 instances using tags
- Install a database (MySQL) on discovered instances

---
## 2. Prerequisites

### Control Node (Ansible Machine)
- Linux (Ubuntu preferred)
- Python 3 installed
- Ansible installed
- Internet access
- AWS account

### Target Node (EC2 Instance)
- EC2 instance running
- SSH access enabled
- Security Group allows port 22
- Instance tagged properly (e.g., Role=db)

## 3. Install Ansible on ubutnu
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```
## 4. Install AWS CLI
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```
```bash
sudo apt install unzip
unzip awscliv2.zip
```
```bash
sudo ./aws/install
```
---
### Verify:
```bash
ansible --version
```
<img width="1597" height="326" alt="image" src="https://github.com/user-attachments/assets/674a7b1b-452c-47b5-9fbd-370c5ae779e5" />
```bash
aws --version
```
<img width="1068" height="61" alt="image" src="https://github.com/user-attachments/assets/e1220a34-2dba-4a69-bc08-e7c45827cfb5" />
```bash
python3 --version
```
<img width="839" height="103" alt="image" src="https://github.com/user-attachments/assets/d5df5834-d544-45bc-a8b9-f30482284431" />

---
## 4. Configure AWS Credentials
Install AWS SDK libraries required for dynamic inventory:
```bash
sudo apt install python3-pip
pip3 install boto3 botocore
```
### Configure AWS CLI
```bash
aws configure
```
Provide:

- AWS Access Key

- AWS Secret Key

- Region (example: ap-south-1)

- Output format (json)

<img width="1005" height="185" alt="image" src="https://github.com/user-attachments/assets/c9d2d109-cc49-4d83-87ec-de1cc969fbb4" />

---
## 5. Enable Dynamic Inventory Plugin
Create or edit Ansible configuration file:
```bash
nano ansible.cfg
```
Add:
```bash
[inventory]
enable_plugins = aws_ec2
```
<img width="805" height="141" alt="image" src="https://github.com/user-attachments/assets/74c7674b-5ec2-4214-b867-bab6cc12b075" />

---
## 6. Create Dynamic Inventory File
Create inventory configuration file:
```bash
nano aws_ec2.yml
```
```bash
plugin: aws_ec2
regions:
  - ap-south-1

filters:
  instance-state-name: running

keyed_groups:
  - key: tags.Role
    prefix: role

compose:
  ansible_host: public_ip_address
```
📌 Explanation

- Fetches running EC2 instances

- Groups instances by tag Role

- Uses public IP for SSH

## 7. Test Dynamic Inventory
```bash
ansible-inventory -i aws_ec2.yml --graph
```
Expected output:
```bash
@all:
  |--@role_db
      |--ec2-xx-xx-xx.compute.amazonaws.com
```
<img width="1908" height="331" alt="image" src="https://github.com/user-attachments/assets/48d7d38e-a1a9-4e3e-9662-6f732d039e5d" />

---
## 8. Verify Connectivity
```bash
ansible all -i aws_ec2.yml -m ping -u ubuntu --private-key key.pem
```
Expected:
```bash
SUCCESS => {"ping": "pong"}
```
<img width="1900" height="837" alt="image" src="https://github.com/user-attachments/assets/6d476227-ece0-4c38-a839-9cd523a2fe72" />

---
## 9. Install Database Using Dynamic Inventory
### Create MySQL Installation Playbook
```bash
nano install_mysql.yml
```
```bash
- name: Install MySQL Database
  hosts: role_db
  become: yes

  tasks:
    - name: Update system packages
      apt:
        update_cache: yes

    - name: Install MySQL Server
      apt:
        name: mysql-server
        state: present

    - name: Start and enable MySQL service
      service:
        name: mysql
        state: started
        enabled: yes
```
---
## 10. Run the Playbook
```bash
ansible-playbook -i aws_ec2.yml install_mysql.yml -u ubuntu --private-key key.pem
```

---
## 11. Verify Database Installation
SSH into EC2:
```bash
ssh -i key.pem ubuntu@<EC2_PUBLIC_IP>
```
Check MySQL status:
```bash
systemctl status mysql
```
<img width="1499" height="491" alt="image" src="https://github.com/user-attachments/assets/61558bad-21e2-408f-946c-028134d9c1a2" />











