# Week 3 – VPC Components Comparisons

# 1. Public and Private Subnets

A subnet name does not make it public or private.

| Route table | Routes | Associated subnets |
|---|---|---|
| Public (`cloudadhar-public-rt`) | local + `0.0.0.0/0 -> IGW` | Public-A, Public-B |
| Private (`cloudadhar-private-rt`) | local only | Private-A, Private-B |
| Main (`cloudadhar-main-rt-local-only`) | local only | No intended lab subnet |

A subnet is public when its route table has a route to an Internet Gateway.
For IPv4 internet communication, an instance also needs a public IPv4 or Elastic
IP and applicable security rules.
