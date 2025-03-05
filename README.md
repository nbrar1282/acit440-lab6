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

### **1️  Build AMI with Packer**
```sh
cd packer
packer init .
packer validate ansible-web.pkr.hcl
packer build ansible-web.pkr.hcl
```
**Note the AMI ID from the output.**

---

### **2️. Deploy EC2 with Terraform**
```sh
cd terraform
terraform init
terraform validate
terraform plan
terraform apply -auto-approve
```
**Retrieve EC2 IP:**  
```sh
terraform output instance_ip_addr
```

---

### **3️ Access EC2 and Deploy Nginx**
```sh
ssh -i /path/to/key.pem ubuntu@<EC2_PUBLIC_IP>
cd ansible
ansible-playbook -i <EC2_PUBLIC_IP>, -u ubuntu --private-key /path/to/key.pem playbook.yml
```
Visit `http://<EC2_PUBLIC_IP>` to see the web page.

---

### **4️ Cleanup**
```sh
terraform destroy -auto-approve
aws ec2 deregister-image --image-id <AMI_ID>
```

---



---

🚀 **Now your README is concise and complete!**
