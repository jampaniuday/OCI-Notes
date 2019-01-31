
# OCI-Networking

OCI Networking Details

---

## IP Ranges

Recommendations as per RFC 1918

- 10.0.0.0/8
- 172.16/12
- 192.168/16

Allowable OCI VCN size range is from /16 to /30

ed.  This seems to conflict with instructions to use RFC 1918, as the largest OCI VCN supported is /16

## Reserved Addresses

These are networking standards.

- n.n.n.0
- n.n.n.1
- n.n.n.LAST

Where LAST is the final address in a subnet range (not necessarily 255)

## Route Tables

Route traffic out of the VCN

There is one Route Table per subnet.

It is used only when the destination is not within current CIDR block.

Routing Rules consist of:

- Destination CIDR block
- Route Target (the next hop) for the traffic that matches that CIDR

## Subnets

Subnets are contained within an AD (Availability Domain)

Private: instances contain private IP addresses assigned to vNICs

Public:

- contain both private and public IP addresses assigned to vNICs
- requires access to an Internet Gateway

---
