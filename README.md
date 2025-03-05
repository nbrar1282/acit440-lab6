# **ACIT 4640 - AWS EC2 Deployment with Packer & Terraform**

## **Overview**
This repository automates EC2 deployment using **Packer** (AMI creation), **Terraform** (infrastructure), and **Ansible** (server configuration).

---

## **Prerequisites**
- **AWS CLI**, **Packer**, **Terraform**, and **Ansible** installed  
- **AWS Key Pair** created (`aws ec2 create-key-pair --key-name my-key`)  
- **AWS credentials** configured (`aws configure`)  

---

## **Deployment Steps**

### **1️⃣ Build AMI with Packer**
```sh
cd packer
packer init .
packer validate ansible-web.pkr.hcl
packer build ansible-web.pkr.hcl
