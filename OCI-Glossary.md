
# OCI Glossary

Also see [OCI - Key Concepts and Terminology](https://docs.cloud.oracle.com/iaas/Content/GSG/Concepts/concepts.htm)

## Autonomous

## ADW

Autonomous Data Warehouse

### ATP

Autonomous Transaction Processing

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

## Networking

### Off Box Networking

Networking optimized to push networking from the Virtual Layer to the Hardware layear.

The performance impact imposed by VM use is very low

### LB

Load Balancing

### VCN

Virtual Cloud Network

### VPN

Virtual Private Network

## Security

Be default, everything is denied.  There are no default privileges

### Compartments

A collection of OCI Resources.

A Tenancy has a _Root_ compartment initially by default.

### Groups

Collection of users that need same type of access to a Resource or set of Resources

### IAM

Identity and Access Management

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
