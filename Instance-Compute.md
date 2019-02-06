# Compute

## Bare Metal

As it says, running on a physical server.  0% overhead due to running in the cloud

Bare Metal has local NVMe storage.

Use Cases:

- Workloads that are Performance-intensive
- Workloads that are not virtualized
- Workloads that require a specific hypervisor
- Workloads that require BYO Licensing


### AMD EPYC Based instances

$0.03 core/hour

Much lower cost than many others.

A 64 core machine with 512G RAM is $1.92 per hour

- hour     1.92
- day     46.08
- week   322.56
- month 1382.40

## Boot Volumes

A Boot Volume is the storage for the image used to boot an instance.

It is used for both Bare Metal and Virtual Machines.

- Boot volume is created automated and associated with an instance until you terminate the instance
- Boot volumes are encrypted, have faster performance, lower launch times, and higher durability for BM and VM instances
- Compute instance can be scaled to a larger shape by using boot volumes
- You can preserve the boot volume when you terminate a compute instance
- Boot volumes are only terminated when you manually delete them
- Boot volumes cannot be detached from a running instance
- Possible to take a manual backup, assign backup policy or create clone of boot volumes

## Instance Life Cycle

Terms:

- Start – Restarts a stopped instance. After the instance is restarted, the Stop action is enabled 
- Stop – Shuts down the instance. After the instance is powered off, the Start action is enabled
- Reboot – Shuts down the instance, and then restarts it
- Terminate – Permanently delete instances that you no longer need (vNICs and volumes are auto detached; boot volume is not deleted, but you can delete it)

Resource Billing

- Standard VM and BM instances, billing pauses in a STOP state
- High I/O BM instances and dense I/O BM and VM instances , billing continues even in STOP state

Local storage incurs billing, even in a stopped state.

## Instance Metadata

This is cool.

- Instance Metadata includes its OCID, name, compartment, shape, region, AD, creation date, state, image, and any custom metadata such as an SSH public key
- Service runs on every instance and is an HTTP endpoint listening on 169.254.169.254
- Get instance metadata by logging in to the instance and using the metadata service

Oracle provided Linux instances

- curl http://169.254.169.254/opc/v1/instance/
- curl http://169.254.169.254/opc/v1/instance/metadata/
- curl http://169.254.169.254/opc/v1/instance/metadata/<key-name>/

Add and update custom metadata for an instance using CLI or SDK

## Virtual Machine

A compute instance (eg Linux) running on a hypervisor.

Virtual instances run on the same type hardware as Bare Metal instances.  The API's are the same, so decision to run a 40 Core Bare Metal machine or a 1 core VM can be decided by MetaData.

There is no local storage.

### Images

The user name _opc_ is created automatically when Oracle Provided images are used.

Ubuntu is an exception as the default user is _ubuntu_.

Custom images cannot exceed 300G.

Custom images supports:

- Paravirtualized:  !Needs Definition!
- Emulation Mode:  Fully emulated NIC, block boot, legacy BIOS.
- Native Mode: Offer maximum performance with modern OS’s

Native mode is the method of choice.

No cost to store custom images, up to 25 per compartment.  Cool!

See [Deploying Custom Operating System Images on Oracle Cloud Infrastructure](https://cloud.oracle.com/iaas/whitepapers/deploying_custom_os_images.pdf "Custom OS Images")

### Instance Configuration and Pool

Create sets of configuration parameters used to launch an instance.

This Instance Configuration serves as a template to launch an instance.

A Pool allows provising and creating multiple instances based on the same Instance Configuration

Pool:Congiguration is 1:1

A single Configuration may be used on multiple pools.







