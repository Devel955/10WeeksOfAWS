# Week 3 - Day 6: Amazon VPC Part 2

## Name

Anand Sen

## Tasks Completed

- [x] Watched/read the weekly content
- [x] Extended the VPC
- [x] Completed hands-on labs
- [x] Added screenshots or proof
- [ ] Posted on LinkedIn
- [ ] Cleaned up AWS resources

---

## Architecture

> The architecture diagram will be added here when it is ready.

```text
Internet
   |
Internet Gateway
   |
Public Subnet (10.10.0.0/24)
   |-- Public EC2 web server (HTTP :80)
   |-- NAT Gateway
   |
Private Subnet (10.10.12.0/24)
   |-- Private EC2 (no public IPv4)
   |-- EC2 Interface Endpoint (Private DNS)
   |
   +-- S3 Gateway Endpoint --> Amazon S3
```

---

## Architecture Decisions

### Why use a NAT Gateway?

- Allows the private EC2 instance to access the internet without assigning it a public IPv4 address.
- Keeps inbound internet traffic away from private workloads.
- Uses a public subnet, Internet Gateway, and Elastic IP to provide secure outbound connectivity.

### Why use an S3 Gateway Endpoint?

- Allows private instances to access **Amazon S3** without using the public internet.
- Avoids NAT Gateway data processing charges for S3 traffic.
- Keeps S3 traffic on the **AWS network**.
- Supports endpoint policies for restricting bucket access.

### Why use an EC2 Interface Endpoint?

- Enables private access to the EC2 API from inside the VPC.
- Private DNS resolves the regional EC2 API hostname to the endpoint network interface.
- Allows the private instance to communicate with AWS services without public routing.

---

## Result

Extended the Day 5 VPC with secure outbound internet access, private AWS service connectivity, subnet-level filtering, and network traffic monitoring.

**Resources created:**

- NAT Gateway: `clouddhar-day6-vpc`
- Elastic IP for the NAT Gateway
- Private Route Table: `clouddhar-private-rt`
- Amazon Linux 2023 private EC2 instance: `clouddhar-private-ec2-a`
- Public EC2 web server: `clouddhar-web-ec2-a`
- Custom Network ACL: `clouddhar-custom-nacl`
- Amazon S3 Gateway Endpoint: `clouddhar-s3-gateway-endpoint`
- Amazon EC2 Interface Endpoint: `clouddhar-ec2-interface-endpoint`
- VPC Flow Logs with a CloudWatch Logs destination

**Validation:**

- Private EC2 has no public IPv4 address.
- Session Manager access is online and connected.
- Internet connectivity works through the NAT Gateway.
- AWS CLI authentication is successful through the instance IAM role.
- HTTP is allowed by the web server security group.
- Temporary NACL deny rules block HTTP traffic.
- Restoring the NACL rules restores connectivity.
- Amazon S3 traffic uses the Gateway Endpoint prefix-list route.
- The EC2 API resolves through the Interface Endpoint using Private DNS.
- VPC Flow Logs record both `ACCEPT` and `REJECT` traffic.

---

### 1. NAT Gateway Available

![NAT Gateway Available](./screenshots/NAT%20Gateway%20Available.png)

---

### 2. Private-A Route Table

![Private-A Route Table](./screenshots/Private-A%20Route%20Table.png)

---

### 3. Public Route Table

![Public Route Table](./screenshots/Public%20Route%20Table.png)

---

### 4. Private EC2 Instance

![Private EC2 Instance](./screenshots/Private%20EC2%20Instance.png)

---

### 5. Session Manager Connection

![Session Manager Connection](./screenshots/Session%20Manager%20Connection.png)

---

### 6. Internet Connectivity Validation

![Internet Connectivity Validation](./screenshots/Internet%20Connectivity%20Validation.png)

---

### 7. AWS CLI Identity Validation

![AWS CLI identity Validation](./screenshots/AWS%20CLI%20identity%20Validation.png)

---

### 8. Web Server Security Group

![Web Server Security Group](./screenshots/Web%20Server%20Security%20Group.png)

---

### 9. Web Server Running

![Web Server Running](./screenshots/Web%20Server%20Running.png)

---

### 10. Custom Network ACL

![Custom Network ACL](./screenshots/Custom%20Network%20ACL.png)

---

### 11. HTTP Blocked by Network ACL

![HTTP Blocked by Network ACL](./screenshots/HTTP%20Blocked%20by%20Network%20ACL.png)

---

### 12. HTTP Restored

![HTTP Restored](./screenshots/HTTP%20Restored.png)

---

### 13. Amazon S3 Gateway Endpoint

![Amazon S3 Gateway Endpoint](./screenshots/Amazon%20S3%20Gateway%20Endpoint.png)

---

### 14. S3 Prefix List Route

![S3 Prefix List Route](./screenshots/S3%20Prefix%20List%20Route.png)

---

### 15. Amazon S3 Validation

![Amazon S3 Validation](./screenshots/Amazon%20S3%20Validation.png)

---

### 16. EC2 Interface Endpoint

![EC2 Interface Endpoint](./screenshots/EC2%20Interface%20Endpoint.png)

---

### 17. Private DNS Resolution

![Private DNS Resolution](./screenshots/Private%20DNS%20Resolution.png)

---

### 18. VPC Flow Logs Configuration

![VPC Flow Logs Configuration](./screenshots/VPC%20Flow%20Logs%20Configuration.png)

---

### 19. Flow Logs – REJECT Traffic

![Flow Logs – REJECT Traffic](./screenshots/Flow%20Logs%20%E2%80%93%20REJECT%20Traffic.png)

---

### 20. Flow Logs – ACCEPT Traffic

![Flow Logs - ACCEPT Traffic](./screenshots/Flow%20Logs%20-%20ACCEPT%20Traffic.png)

---

### 21. AWS VPC Resource Map

![AWS VPC Resource Map](./screenshots/AWS%20VPC%20Resource%20Map.png)

---

## Where I Got Stuck

`No blocker`

---

## Cleanup

**Cleanup (in order):**

1. Terminate the Day 6 EC2 instances.
2. Delete the EC2 Interface Endpoint.
3. Delete the NAT Gateway and wait for deletion to complete.
4. Release the Elastic IP.
5. Delete the S3 Gateway Endpoint if it is no longer needed.
6. Delete the VPC Flow Log.
7. Delete the dedicated CloudWatch Logs group if it is no longer needed.
8. Restore the original NACL association.
9. Delete the custom Network ACL.
10. Remove temporary route tables and security groups.

---

## LinkedIn Post

To be added.

