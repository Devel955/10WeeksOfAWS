# Day 5 — Two-AZ VPC Fundamentals (Part 1)

## Learner
Anand Sen

## Objective
Build a custom VPC in Mumbai with two public and two private subnets across two Availability Zones. The public subnets route to an Internet Gateway, while the private subnets have no IPv4 internet path in Part 1.

## Architecture

![Two-AZ VPC architecture](diagrams/two-az-vpc-architecture.png)

## Build Summary

| Component | Configuration |
|---|---|
| Region | `ap-south-1` (Mumbai) |
| VPC | `cloudadhar-day5-vpc` — `10.10.0.0/16` |
| Internet Gateway | `cloudadhar-day5-igw` |
| Public route table | `cloudadhar-public-rt` |
| Private route table | `cloudadhar-private-rt` |
| Main route table | `cloudadhar-main-rt-local-only` |

## CIDR Plan

| Subnet | Availability Zone | CIDR | Public IPv4 assignment |
|---|---|---|---|
| `cloudadhar-public-a` | `ap-south-1a` | `10.10.1.0/24` | Enabled |
| `cloudadhar-private-a` | `ap-south-1a` | `10.10.11.0/24` | Disabled |
| `cloudadhar-public-b` | `ap-south-1b` | `10.10.2.0/24` | Enabled |
| `cloudadhar-private-b` | `ap-south-1b` | `10.10.12.0/24` | Disabled |

All four ranges are inside the VPC CIDR and do not overlap.

## Routing Result

- The main route table is local-only and has no explicit lab subnet association.
- The public route table has `0.0.0.0/0` to the Internet Gateway and is associated with both public subnets.
- The private route table has only the VPC local route and is associated with both private subnets.
- No EC2 instance or NAT Gateway was created in this cost-safe Part 1 lab.

## Evidence

### VPC Created
![VPC created](screenshots/01_vpc_created.png)

### Subnets Created
![Subnets created](screenshots/02_subnets_created.png)

### Internet Gateway Attached
![Internet Gateway attached](screenshots/03_igw_attached.png)

### Main Route Table
![Main route table](screenshots/04_main_route_table.png)

### Public Route Table
![Public route table](screenshots/05_public_route_table.png)

### Private Route Table
![Private route table](screenshots/06_private_route_table.png)

### Final VPC Resource Map
![VPC resource map](screenshots/07_vpc_resource_map.png)

## What I Learned
A subnet is public because of its route table and a route to an Internet Gateway, not because of its name. Explicit route-table associations make the intended public/private traffic policy clear.

## Cost and Safety
No EC2 instance and no NAT Gateway were created. The VPC is retained for the next lab.
