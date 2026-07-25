# CIDR Plan

The VPC uses `10.10.0.0/16`, giving 65,536 total IPv4 addresses. Each `/24` subnet contains 256 addresses; AWS makes 251 usable addresses available in each subnet.

| Network | CIDR | Purpose |
|---|---|---|
| VPC | `10.10.0.0/16` | Overall lab network |
| Public A | `10.10.1.0/24` | First-AZ public subnet |
| Public B | `10.10.2.0/24` | Second-AZ public subnet |
| Private A | `10.10.11.0/24` | First-AZ private subnet |
| Private B | `10.10.12.0/24` | Second-AZ private subnet |

The four subnet ranges are distinct, non-overlapping, and inside the VPC range.
