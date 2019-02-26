
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

## Database

OCI Database Services (not necessarily just Oracle DB)

---

## Infrastructure Architectures

### Availability Domain (AD)

Fully Independent Datacenters within a Region
See Fault Domain

### Fault Domain (FD)

Localized independent HW and Infrastructure within a Domain
See Availability Domain

### Region

Geographical Data Center Location

See Availability Domain and Fault Domain

---

## General

### Billing

Both Soft (generate alert) and Hard (no new services, current services suspended) limits can be set per Service Category.

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

### Tagging

Resource tags can be used to easily identify related resources.

See [Resource Tags](https://docs.cloud.oracle.com/iaas/Content/General/Concepts/resourcetags.htm "Resource Tags")

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

### Load Balancer

The OCI Load Balancing Service - distribute the load of incoming requests among 2 or more servers.

Chief Benefits are Scaling and High Availability

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

Security Lists are a lists of firewall security rules that belong to a VCN

Security lists can be applied to  subnet allowing/disallowing network  egress/ingress from the subnet

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

By default, everything is denied.  There are no default privileges


### Compartments

A collection of OCI Resources.

A Tenancy has a _Root_ compartment initially by default.

### Groups

Collection of users that need same type of access to a Resource or set of Resources

### HSM

Hardware device dedicated to key management

[Hardware Security Module](https://en.wikipedia.org/wiki/Hardware_security_module "Hardware Security Module")

### IAM

Identity and Access Management

### IdP

Identity Provider - used at sign in to the console. This is Oracle Identity Cloud Service by default.

### Instance Principals

Instance Principals allows instances (and applications) to make API calls against other OCI services removing the need to configure user credentials or a configuration file

### KMS

[KMS FAQ - Key Management Service](https://cloud.oracle.com/cloud-security/kms/faq "KMS - Key Management Service")

### Policies

Collection of privileges

Can only be 'allowed'  to Groups - not to Users

Policies can be attached to Compartments or the Tenancy (ed. may need revision)

Format: _Allow \<subject\> to \<verb\> \<resource-type\> in \<location\> where \<conditions\>_

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

---

## Storage

### Block Storage Types

Block Volumes and Local Storage on OCI are NVMe based and are organized into 4k blocks.

### Boot Volume

Boot Volumes persist instance termination, and may be used to start a new instance, or to stop an instance, scale it larger and restart.

### Clone

Block Volumes may be cloned via disk to disk copy.

### Crash Consistent

A backup that is made via Volume Snapshots (clone).  A crash consistent backups is one where the files are all backed up to the exact same moment in time.

### Ephemeral Storage

Local storage that does not survive instance termination.

### FSS

File System Service - NFSv3 Compatible

### IOPS

Input/Output Operations Per Second.  A Performance metric for storage.

### Latency

The amount of time required to service a request.  < 1 millisecond for NVMe

### Mount Targets

An OCI Object created in an AD: it is used to control access to up to 100 FSS.

### NVMe

Non-Volatile Memory Express.  Fast SSD that is attached directly to the PCIe bus.

### Object Storage

High performance storage for an unlimited amount of unstructured data.

### PCIe

Peripheral Component Interconnect Express bus

### Persistant Storage

Persistant storage that survives instance termination

### Volume Groups

A grouping of Boot and Block Volumes that can be operated on as a group, such as with backups and clones.
