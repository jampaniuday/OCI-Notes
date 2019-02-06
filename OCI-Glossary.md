
# OCI Glossary

Also see [OCI - Key Concepts and Terminology](https://docs.cloud.oracle.com/iaas/Content/GSG/Concepts/concepts.htm)

---

## Autonomous

### ADW

Autonomous Data Warehouse

### ATP

Autonomous Transaction Processing

---

## Compute

### Bare Metal

As it says, running on a physical server.  0% overhead due to running in the cloud

### Virtual Machine

A compute instance (eg Linux) running on a hypervisor.

---

## Infrastructure Architecture

### Availability Domain (AD)

Fully Independent Datacenters within a Region 
See Fault Domain

## Fault Domain (FD)

Localized independent HW and Infrastructure within a Domain
See Availability Domain

## Region

Geographical Data Center Location

See Availability Domain and Fault Domain

---

## General

### DBMS_Cloud

A PL/SQL package for use with autonomous services

See [DBMS_CLOUD Package – A Reference Guide](https://antognini.ch/2018/07/dbms_cloud-package-a-reference-guide/)

### OCI

Oracle Cloud Infrastructure

### OCID

Oracle Cloud Infrastructure ID

This is a unique identifier

### Resource

Any cloud object created in OCI

Each OCI Resource is identified by a unique OCID

### Tenancy

When you sign up for Oracle Cloud Infrastructure, Oracle creates a tenancy for your company, which is a secure and isolated partition within Oracle Cloud Infrastructure where you can create, organize, and administer your cloud resources.

---

## Networking

### BPG

Border Gateway Protocol

### CPE

Customer Premises Equipment

### DNS Domain Name System

OCI uses its own Internal DNS

### Dynamic Routing Gateway

A virtual router used to route traffic to destinations other than the internet.

### FastConnect

A direct and private connection between OCI and your non-OCI Data Center.

### FQDN

Fully Qualified Domain Name

### Local Peering Gateway

An LPG is used to connect two VCNs in the same region.

See VCN Peering

### Internet Gateway

A path for network traffic between your VCN and the internet

Allows outbound connections and incoming connections

Only 1 Internet Gateway is allowed per VCN

### NAT Gateway

A path for network traffic between your VCN and the internet.

Allows iniating traffic from the VCN only.

Allow Private Subnets to reach the Internet

Use case:  getting patches, updates, etc.

### LB

Load Balancing

### Off Box Networking

Networking optimized to push networking from the Virtual Layer to the Hardware layear.

The performance impact imposed by VM use is very low

### Public IP Address

An IP address that can be routed on the internet.

Several OCI objects or services can have a Public IP Address.

### Remote Peering Connection

An RPC is used to connect two VCNs in the different regions; it is created on a Dynamic Routing Gateway (DRG)

See:

- VCN Peering
- See Dynamic Routing Gateway (DRG)

### Route Table

Route Traffic out of the VCN

### Security Lists

Firewall rules per subnet allowing/disallowing network  egress/ingress from the subnet

Rules may be Stateful or Stateless

Security Rules are stateful by default

### Service Gateway

Service Gateway is a pre-existing OCI Gateway for Public OCI Services.

The Service Gateway allows accessing Public OCI services (eg. Object Storage) without an Internet or NAT Gateway

### VCN

Virtual Cloud Network

### VCN Peering

There are 2 types of VCN Peering:

- local VCN Peering
- remote VCN Peering

### VPN

Virtual Private Network

OCI has two options for IPsec VPN connectivity

- OCI managed VPN Service (free)
- Software VPN (running on OCI Compute)

---

## Security

Be default, everything is denied.  There are no default privileges

### Compartments

A collection of OCI Resources.

A Tenancy has a _Root_ compartment initially by default.

### Groups

Collection of users that need same type of access to a Resource or set of Resources

### IAM

Identity and Access Management

### IdP

Identity Provider - used at sign in to the console. This is Oracle Identity Cloud Service by default.

### Instance Principals

Instance Principals allows instances (and applications) to make API calls against other OCI services removing the need to configure user credentials or a configuration file

### Policies

Collection of privileges

Can only be 'allowed'  to Groups - not to Users

Policies can be attached to Compartments or the Tenancy (ed. may need revision)

Format: _Allow <subject> to <verb> <resource-type> in <location> where <conditions>_

Verbs:

- inspect
- read
- use
- manage

Example:

```SQL
Allow group ObjectWriters to manage objects in compartment ABC where any {request.permission='OBJECT_CREATE', request.permission='OBJECT_INSPECT'}

Allow group ObjectWriters to manage objects in compartment ABC where any {request.operation=‘CreateObject', request.operation=‘ListObjects'}

Allow service blockstorage, objectstorage-<region_name> to use keys in compartment ABC

```

### Principals

Some IAM entity that is allowed to interact with OCI Resources

### Users

IAM users and Instance Principals

The Principal may be a User Account or an Application
