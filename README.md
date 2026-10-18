# AWS VPC Peering and Cross-VPC Connectivity

## 🌐 Project Overview

This project demonstrates how to establish and verify secure network connectivity between resources in two isolated Amazon Virtual Private Clouds (VPCs) using **AWS VPC Peering**.

The project connects private instances in separate VPCs, configures routing between the networks, and uses security group rules to control traffic. Connectivity is verified using ICMP ping tests.

## 🏗️ Architecture Details

- **VPC A (`10.10.0.0/16`)**:
  - Bastion Host: `10.10.1.10` (Private IP)
  - App Instance A (`ewb-app-a`): `10.10.2.10`

- **VPC B (`10.20.0.0/16`)**:
  - App Instance B (`ewb-app-b`): `10.20.1.10`

- **Gateway**:
  - AWS VPC Peering Connection (`pcx-xxxxxx`)
  - Enables private IP communication between VPC A and VPC B.

## 🛠️ Configuration Steps Taken

1. **VPC Peering Connection**:
   - Created a VPC peering connection between VPC A and VPC B.
   - Accepted the peering request to activate the connection.

2. **Route Table Configuration**:
   - Updated VPC A's private route table (`ewb-rt-a-private`) with a route to `10.20.0.0/16` through the peering connection.
   - Updated VPC B's private route table (`ewb-rt-b-private`) with a return route to `10.10.0.0/16` through the peering connection.

3. **Security Group Configuration**:
   - Configured the security group associated with `ewb-app-b` to allow inbound **ICMP - IPv4 (Echo Request)** traffic from VPC A (`10.10.0.0/16`).
   - Restricted permitted traffic to the required source network.

4. **Connectivity Testing**:
   - Connected to `ewb-app-a` through SSH.
   - Used the `ping` command to test connectivity to `ewb-app-b` using its private IP address.

## ✅ Verification & Results

- Successfully established a VPC peering connection between the two VPCs.
- Configured routes in both VPCs to enable communication between their private networks.
- Verified connectivity by sending ICMP echo requests from `ewb-app-a` to `ewb-app-b`.
- Demonstrated private network communication without requiring public IP addresses for communication between the application instances.

## 🔐 Security Considerations

- Used private IP addresses for communication across the peered VPCs.
- Configured security group rules to allow only the required traffic.
- Avoided opening SSH access to `0.0.0.0/0`; restrict SSH to trusted source IPs or approved network paths.
- Followed the principle of least privilege when configuring network access.

## 📚 AWS Services Used

- Amazon VPC
- AWS VPC Peering
- Amazon EC2
- VPC Route Tables
- Security Groups
- ICMP and SSH

## 🚀 Key Learnings

- Understanding VPC isolation and private IPv4 addressing.
- Establishing connectivity between separate VPCs using VPC Peering.
- Configuring route tables for forward and return traffic.
- Using security groups to control inbound and outbound traffic.
- Troubleshooting private network connectivity with SSH and ping.

## 🔮 Future Improvements

- Configure VPC Flow Logs for network traffic monitoring.
- Test connectivity between additional private instances.
- Automate VPC and peering configuration using Terraform.
- Document route table and security group configurations with screenshots.


