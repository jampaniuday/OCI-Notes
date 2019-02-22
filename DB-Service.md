# Database Service

## Autonomous Database

Actually this is 2 services

- Autonomous Data Warehouse (ADW)
- Autonomous Transaction Processing (ATP)

[Autonomous Database](https://github.com/jkstill/OCI-Notes/blob/master/DB-Autonomous.md "Autonomous Database")


---

## Features

Available architectures

- Exadata
- RAC (2 node only at this time)
- Data Guard
- BYOL if you like (Bring Your Own License)
- Automated Backups
- Encryption
- Automated Patching

---

## Virtual Machines

Platform | CPU Core|Memory|Storage|Network|RAC Interconnect|Nodes
---------|---------|------|-------|-------|----------------|------
VM (X5)|16|7-112 GB|256GB - 40 TB|0.6- 4.8 Gbps|0.6-4.8 Gbps|2
VM (X7)|24|15-320 GB|256GB - 40 TB|1- 24.6 Gbps|1-24.6 Gbps|2

### Storage

- ASM Block Storage
- DATA and RECO Disk Groups


--- 

## Bare Metal

Platform | CPU Core|Memory|Storage|Network|Nodes
---------|---------|------|-------|-------|-----
Oracle Linux 6.8|36-52 cores|512-768M RAM|28-51TB NVME|10-25 Gbps|1

- 12c+ uses ASM for database files
- 11g uses ACFS for database files

- NVMe local storage
- DATA and RECO Disk Groups

---

## Exadata

See the options and pricing on the website - too many options to reproduce here:

[Exadata Cloud Options](https://cloud.oracle.com/en_US/database/exadata/pricing "Exadata Cloud Options")



---


