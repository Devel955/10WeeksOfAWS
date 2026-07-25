# Routing Decisions

## Public and private subnets

| Aspect | Public subnet | Private subnet |
|---|---|---|
| Default route | `0.0.0.0/0` to an Internet Gateway | No default IPv4 internet route in Part 1 |
| Public IPv4 assignment | Enabled for the two public subnets | Disabled |
| Intended use | Internet-facing components when required | Internal application or data components |
| Direct internet path | Available through the public route table | Not available in this lab |

## Why use separate route tables?

Dedicated route tables make the traffic policy explicit. Both public subnets share the same public route table, which contains the IGW route. Both private subnets share a local-only route table. This design prevents the private subnets from gaining internet access merely because an IGW exists in the VPC.

## Why retain a local-only main route table?

The main route table is left as a safe fallback. All lab subnets are explicitly associated with public or private route tables, so their intended routing does not depend on the main table.
