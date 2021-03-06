
# OCI-Networking

OCI Networking Details

---

## Routing and Naming

### BPG

Border Gateway Protocol

This is the protocol used to route traffic on the backbone between networks.

### DNS Domain Name System

Also see [DNS](https://github.com/jkstill/OCI-Notes/blob/master/Net-DNS.md "DNS")

OCI uses its own Internal DNS

Options:

Internet and VCN Resolver: default choice for new VCNs

Custom Resolver: lets instances resolve the hostnames in on-premise network

A DNS label may be specified when creating VCN/subnets/instances

DNS Names

- VCN: _VCN DNS label.oraclevcn.com_
- Subnet: _subnet DNS label.VCN DNS label.oraclevcn.com_
- Instance FQDN: _hostname.subnet DNS label.VCN DNS label.oraclevcn.com_
- Instance FQDN resolves to the instance's Private IP address

Public IP addresses created in a VCN do not automatically get an FQDN assigned.

ie. when using SSH to connect remotely, you will need to use an IP address or external-to-OCI name resolution

### Dynamic Routing Gateway

Use a Dynamic Routing Gateway to route traffic to your on prem or colo, etc.

Connect with IPsec VPN or FastConnect

The DRG is a stand-alone object and has a 1:1 relationship with a VCN.

- There can be only 1 DRG attached to a VCN
- A DRG cannot be attached to more than 1 VCN

See FastConnect

### FastConnect

A direct and private connection between OCI and your non-OCI Data Center.

The connection can be 1G of 10G.

### Internet Gateway

Only 1 Internet Gateway is allowed per VCN

A Gateway is not required to access Public OCI Services such as Object Storage - see Service Gateway

### Local Peering Gateway

An LPG is used to connect two VCNs in the same region.

An LPG is not a standalone object.  Each of the VCNs to be connected must have an LPG.

The LPGs cannot have overlapping CIDR blocks.

See VCN Peering

### NAT Gateway

Multiple NAT Gateways allowed per VCN.

A subnet can route traffic to only 1 NAT Gateway.
( only 1 0.0.0.0/0 route per subnet)

A Gateway is not required to access Public OCI Services such as Object Storage - see Service Gateway

## Route Tables

Route traffic out of the VCN

There is one Route Table per subnet.

It is used only when the destination is not within current CIDR block.

Routing Rules consist of:

- Destination CIDR block
- Route Target (the next hop) for the traffic that matches that CIDR

### Service Gateway

Service Gateway traffic never traverses the internet (are there any exceptions?)

This traffic is on the OCI Fabric

## IP Addressing

### IP Ranges

Recommendations as per RFC 1918

- 10.0.0.0/8
- 172.16/12
- 192.168/16

Allowable OCI VCN size range is from /16 to /30

ed.  This seems to conflict with instructions to use RFC 1918, as the largest OCI VCN supported is /16

### Public IP Address

An IP address that can be routed on the internet.

Two types of Public IP:

- ephemeral - exists only for the lifetime of the instance
- reserved - persists and can be re-assigned to other instances

Several OCI objects or services can have a Public IP Address.

- Instance (not recommended in most cases)
- OCI Public Load Balancer
- - Internet Gateway
- NAT Gateway
- DRG – IPsec tunnels
- Autonomous Data Warehouse
- Autonomous Transaction Processing
- OKE (Kubernetes) cluster master and worker nodes

Public IP Addresses are assigned by Oracle and cannot be changed.

### Remote Peering Connection

An RPC is used to connect two VCNs in the different regions.

An RGP (Remote Peering Gateway) is not a standalone object; it is created on a Dynamic Routing Gateway (DRG)

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

## General Network

### Route Tables

Rules to show how traffic can be routed _out_ of the VCN

A Route Table is not required for instances within the same CIDR block.

A Route Table may be attached to multiple subnets, but each subnet can have only 1 Route Table.


### Security Lists

Security Lists are a lists of firewall security rules that belong to a VCN

Security lists can be applied to one or more subnets,  allowing/disallowing network  egress/ingress from the subnet

Security Lists manage connectivity north-south (incoming/outgoing VCN traffic) and east-west (internal VCN traffic between multiple subnets)

Each subnet may have up to 5 security lists.

OCI follows a white-list model (you must manually specify white listed traffic flows); By default, things are locked down 

Instances cannot communicate with other instances in the same Subnet, until you permit them to!

Rules may be Stateful or Stateless

Security Rules are stateful by default

Use case for Stateful Rule:

An incoming (ingress) rule may be created for port 80 for an app running via HTTP.

If the rule is stateful, there is no need for an egress rule to allow the outgoing responses - they are allowed by default with Stateful Rules.

A Stateless Rule would not allow this outgoing response without a corresponding egress rule.

Stateless is better for any service or app generating a large number of connections, as that would be too much to track.

ie. Load Balancers, Analytic queries with many connections, etc.

### SR-IOV

Single-Root I/O Virtualization

An optimization to improve networking performance with PCIe devices

[What is SR-IOV?](https://blog.scottlowe.org/2009/12/02/what-is-sr-iov/ "What is SR-IOV?")

### Subnets

Subnets are contained within an AD (Availability Domain)

Each Subnet may have up to:

- 5 Security Lists attached
- 1 Route Table attached

Private: instances contain private IP addresses assigned to vNICs

Public:

- contain both private and public IP addresses assigned to vNICs
- requires access to an Internet Gateway

### VCN Peering

There are 2 types of VCN Peering:

- local VCN Peering
- remote VCN Peering

### VPN

Virtual Private Network

OCI has two options for IPsec VPN connectivity

- OCI managed VPN Service (free)
- Software VPN (running on OCI Compute)
