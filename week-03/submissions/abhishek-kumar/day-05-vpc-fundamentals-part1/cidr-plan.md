# CIDR Plan

The VPC address range is `10.10.0.0/16`. A `/16` contains 65,536 IPv4 addresses; AWS reserves five addresses in a subnet, leaving 65,531 usable addresses at the VPC level.

| Network | CIDR | Total IPv4 addresses | Usable in AWS | Purpose |
|---|---|---:|---:|---|
| VPC | `10.10.0.0/16` | 65,536 | 65,531 | Overall learning environment |
| Public A | `10.10.1.0/24` | 256 | 251 | Public-A in the first AZ |
| Public B | `10.10.2.0/24` | 256 | 251 | Public-B in the second AZ |
| Private A | `10.10.11.0/24` | 256 | 251 | Private-A in the first AZ |
| Private B | `10.10.12.0/24` | 256 | 251 | Private-B in the second AZ |

The address plan leaves room for future subnets while keeping public and private networks easy to identify. The four `/24` ranges are separate and fully contained within the VPC range.
