# Block Storage

## Block Storage Types

Block Volumes and Local Storage on OCI are NVMe based.

These are organized into 4k blocks.

Storage may be _ephemeral_ or _persistent_

- Block Volumes: Persistant storage that survives instance termination
  - Block Volumes may be disconnected and reconnected to another instance without data loss.
- Local NVMe:  Ephemeral storage that does not survive instance termination.

Local NVMe does persist through reboots and pauses of an instance.

## Block Volume

Block Volumes are attached to compute instances via iSCSI or (???)

Storage Size Limit: Petabytes (1 PT I think)

- Capacity Configurable: 50 GB to 32 TB (1GB increments)
- Perf: disk type NVMe SSD based
- Perf: IOPS 60 IOPS/GB - up to 25K IOPS*
- Perf: Throughput/Vol 480 KBPS/GB -  up to 320 MBPS**
- Perf: Latency  Sub-millisecond latencies
- Perf: Per-instance Limits	•32 attachments/instance, up to 1 PB (32 TB/volume x 32 volumes/instance)  - Up to 400K IOPS, near line rate throughput
- Durability: Multiple replicas across multiple storage servers within the AD

## Boot Volume

Boot Volumes persist instance termination, and may be used to start a new instance, or to stop an instance, scale it larger and restart.

## Clone

Block Volumes may be cloned via disk to disk copy.

The clone operation returns immediately while the copy continues in the background.

## Crash Consistent

A backup that is made via Volume Snapshots (clone).  A crash consistent backups is one where the files are all backed up to the exact same moment in time.

## IOPS

Input/Output Operations Per Second.  A Performance metric for storage.

## Latency

The amount of time required to service a request.  < 1 millisecond for NVMe

## NVMe

Non-Volatile Memory Express.  Fast SSD that is attached directly to the PCIe bus.

Storage Size Limit: Terabytes

- Bare Metal: 51.2 T
- Virtual Machine: 25.6 T

## PCIe

Peripheral Component Interconnect Express bus


## Volume Groups

A grouping of Boot and Block Volumes that can be operated on as a group, such as with backups and clones.
These are point-in-time crash consistent backups.

Full or incremental backups may also be taken of a Volume Group
