
# OCI-Networking

OCI Networking Details

---

### Dynamic Routing Gateway

Use a Dynamic Routing Gateway to route traffic to your on prem or colo, etc.

Connect with IPsec VPN or FastConnect

The DRG is a stand-alone object and has a 1:1 relationship with a VCN.

- There can be only 1 DRG attached to a VCN
- A DRG cannot be attached to more than 1 VCN

See FastConnect

### FastConnect

A direct and private connection between OCI and your non-OCI Data Center.

## IP Ranges

Recommendations as per RFC 1918

- 10.0.0.0/8
- 172.16/12
- 192.168/16

Allowable OCI VCN size range is from /16 to /30

ed.  This seems to conflict with instructions to use RFC 1918, as the largest OCI VCN supported is /16

### Internet Gateway

Only 1 Internet Gateway is allowed per VCN

A Gateway is not required to access Public OCI Services such as Object Storage - see Service Gateway

### Local Peering Gateway

An LPG is used to connect two VCNs in the same region.

An LGP is not a standalone object.  Each of the VCNs to be connected must have and LPG.

The LPGs cannot have overlapping CIDR blocks.

See VCN Peering

### NAT Gateway

Multiple NAT Gateways allowed per VCN.

A subnet can route traffic to only 1 NAT Gateway.
( only 1 0.0.0.0/0 route per subnet)

A Gateway is not required to access Public OCI Services such as Object Storage - see Service Gateway

### Remote Peering Connectin

An RPC is used to connect two VCNs in the different regions.

An RGP is not a standalone object; it is created on a Dynamic Routing Gateway (DRG)

The RPCs cannot have overlapping CIDR blocks.

Use Case: Disaster Recovery

See:

- VCN Peering
- See Dynamic Routing Gateway (DRG)

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

### Security Lists

Firewall rules per subnet allowing/disallowing network  egress/ingress from the subnet

Rules may be Stateful or Stateless

Security Rules are stateful by default

Use case for Stateful Rule:

An incoming (ingress) rule may be created for port 80 for an app running via HTTP.

If the rule is stateful, there is no need for an egress rule to allow the outgoing responses - they are allowed by default with Stateful Rules.

A Stateless Rule would not allow this outgoing response.


### Service Gateway

Service Gateway traffic never traverses the internet (are there any exceptions?)

This traffic is on the OCI Fabric

## Subnets

Subnets are contained within an AD (Availability Domain)

Private: instances contain private IP addresses assigned to vNICs

Public:

- contain both private and public IP addresses assigned to vNICs
- requires access to an Internet Gateway

### VCN Peering

There are 2 types of VCN Peering:

- local VCN Peering
- remote VCN Peering



---
