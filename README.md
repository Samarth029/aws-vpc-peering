# AWS VPC Peering and Cross-VPC Connectivity

## 🌐 Project Overview
This project demonstrates how to establish and verify secure, bidirectional network connectivity between two isolated private instances residing in separate Virtual Private Clouds (`VPC A` and `VPC B`) using **AWS VPC Peering**.

## 🏗️ Architecture Details
* **VPC A (`10.10.0.0/16`)**:
  * Bastion Host: `10.10.1.10` (Private IP)
  * App Instance A (`ewb-app-a`): `10.10.2.10`
* **VPC B (`10.20.0.0/16`)**:
  * App Instance B (`ewb-app-b`): `10.20.1.10`
* **Gateway**: AWS VPC Peering Connection (`pcx-xxxxxx`)

## 🛠️ Configuration Steps Taken
1. **VPC Peering Connection**: Created a peering connection between VPC A and VPC B and accepted the request.
2. **Route Tables**: 
   * Updated VPC A's private route table (`ewb-rt-a-private`) to route `10.20.0.0/16` traffic to the peering connection.
   * Updated VPC B's private route table (`ewb-rt-b-private`) to route `10.10.0.0/16` traffic back to the peering connection.
3. **Security Groups**:
   * Configured `ewb-app-b` security group inbound rules to allow **Custom ICMP - IPv4 (Echo Request)** originating from VPC A (`10.10.0.0/16` or specific instance IP).

## ✅ Verification & Results
Successfully validated bidirectional connectivity by logging into `ewb-app-a` via SSH and pinging `ewb-app-b`.

![Ping Success Screenshot](screenshot-ping.png)
