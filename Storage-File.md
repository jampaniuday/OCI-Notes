# File Storage

## FSS

File Storage Service

- NFSv#3 Compativle
- Durable - multiple copies in an AD
- Exabytes+
- Unit size up to 8 Exabytes
- Full POSIX semantics
- Security: 128-bit, data-at-rest encryption for all file systems & metadata

## Limits

Per AD per Account

- 100 file systems
- 2 mount targets

### Mount Targets

An OCI Object created in an AD: it is used to control access to up to 100 FSS.

See [Managing Mount Targets](https://docs.cloud.oracle.com/iaas/Content/File/Tasks/managingmounttargets.htm "Managing Mount Targets")

## Subnets

Place FSS in its own subnet.

IP Addresses are assigned automatically to FSS and cannot be edited.

Do not use a CIDR of less than /29, as /30 leaves only 1 address (OCI reserves 3 addresses)

## Cost

$0.0425 GB/Month, measured hourly & billed monthly

## Can I NFS mount this to an on-premise server?

Yes, via FastConnect or IPsec VPN.

## Security

Security layer | Component | Controls this
---------------|-----------|--------------
IAM Service | OCI users, policies | Creating instances (NFS clients) and FSS VCNs. Creating, listing, and associating file systems and mount targets
Security Lists | CIDR blocks | Connecting the NFS client instance to the mount target
Export Options | Export options, CIDR blocks | Applying access control per-file system based on source IP CIDR blocks that bridges the Security Lists layer and the NFS v.3 Unix Security layer
NFS v3. Unix Security | Unix users | Mounting file systems1, reading the writing files, file access security 

Note: When mounting file systems, don't use mount options such as nolock, rsize, or wsize. These options cause issues with performance and file locking

If managed with Security Lists then the client has access to all or none FSS.

Using Export Options instead can allow access per FSS.

##  Ports

These ports must be open for the client to access the FSS.

Type | Source CIDR | Protocol | Source Port | Dest Port
-----|-------------|----------|-------------|----------
Ingress | 10.0.0.0/24 | TCP | All | 2048-2050
Ingress | 10.0.0.0/24 | TCP | All | 111
Ingress | 10.0.0.0/24 | UDP | All | 2048
Ingress | 10.0.0.0/24 | UDP | All | 111

## Summary Address

Say you have NFS clients in 10.0.1.0 and 10.0.2.0.

Rather than create 2 sets for rules for each subnet, create the rules for the summary address of 10.0.0.0/16


