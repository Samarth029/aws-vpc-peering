# AWS VPC Peering Implementation Steps

## 1. Environment Setup
* Created **VPC A** (`10.10.0.0/16`) with a public subnet (for the Bastion host) and a private subnet (for App Instance A).
* Created **VPC B** (`10.20.0.0/16`) with a private subnet (for App Instance B).

## 2. VPC Peering Configuration
* Initiated a VPC Peering connection request from VPC A to VPC B.
* Accepted the peering request from the VPC B console to establish the connection link.

## 3. Route Table Updates
* **VPC A Private Route Table**: Added a route pointing destination `10.20.0.0/16` to the VPC Peering connection ID.
* **VPC B Private Route Table**: Added a route pointing destination `10.10.0.0/16` to the VPC Peering connection ID.

## 4. Security Group Hardening
* Updated the Security Group for App Instance B in VPC B to allow inbound **ICMP (Echo Request)** traffic originating from VPC A's CIDR (`10.10.0.0/16`).

## 5. Verification
* Logged into the Bastion host, hopped via SSH to App Instance A, and executed a ping test to App Instance B (`10.20.1.10`) to confirm successful bidirectional connectivity with 0% packet loss.
