# Object Storage

High performance storage for an unlimited amount of unstructured data.

From within a VCN Object Storage can be reached via Service Gateway. eg. for use with backups, etc.

## Buckets

A logical container for storing objects: all objects are stored in buckets.

Bucket names are unique only within a tenancy.

This is in contrast with AWS where bucket names must be unique across the entire AWS Infrastructure.

ie. in OCI two different companies (different tenancies) can have a bucket with the same name.

There is no directory structure, it must be simulated if needed.

## Namespace

Each tenancy has a single unique namespace that is global across all compartments and regions.

## Objects

All data is referred to as an object

## Storage Classes

Two storage classes

- Standard Tier (hot): frequently accessed storage
- Archive Tier (cold): infrequently accessed storage
  - minimum retention time is 90 days
  -- TTFB - time to first byte is 4 hrs

## Object Access

Object storage is accessed via Storage Gateway on the Oracle Backbone.

## Hierarchy

There are no directory structures in Object Storage.

A directory may be simulated by the use of hierarchies.

In simple terms, a hierarchy is created by using the literal '/' character in the object name.

Objects may then be operated on from the CLI as if they were in a directory.

Consider the following objects

- data/file-01.dbf
- data/file-02.dbf
- data/file-03.dbf
- pics/pic-01.png
- pics/pic-02.png
- pics/pic-03.png

The '/' does not represent a directory, but is actually part of the object name.

See the documentation for more:

[Object Naming Using Prefixes and Hierarchies](https://docs.cloud.oracle.com/iaas/Content/Object/Tasks/managingobjects.htm#Prefixes "Prefixes and Hierarchies")


## Object Naming

Service prepends the Object Storage namespace string and bucket name to object name.

object_storage_namespace is most likely the Tenancy

- endpoint: URL to region:AD
- n: name
- b: bucket
- o: object

```html
/n/<object_storage_namespace>/b/<bucket>/o/<object_name>
```

/n/           Tenancy        /b/ Bucket /o/ objectname

```html
https://objectstorage.us-phoenix-1.oraclecloud.com/n/gse00014346/b/DatabaseBackup/o/database1.dbf
```

                endpoint                          /n/ tenancy   /b/ Bucket Name  /o/ objectname




### Flat hierarchy

There is no directory structure

For large number of objects, use prefixes and hierarchies,

n/ansh8tvru7zp/b/event_photos/o/marathon/finish_line.jpg
/n/ansh8tvru7zp/b/event_photos/o/marathon/participants/p_21.jpg 

You can use the CLI to perform bulk downloads and bulk deletes of all objects at a specified level of the hierarchy, without affecting objects in levels above or below 
E.g. above, you can use CLI to download or delete all objects at the marathon/ level without downloading or deleting objects at the marathon/participants sublevel

## Mulipart Uploads

Upload large objects in parallel.

Invoked from REST API call.

See [Multipart Uploads](https://docs.cloud.oracle.com/iaas/Content/Object/Tasks/usingmultipartuploads.htm "Multipart Uploads")

## Object Lifecycle Management

Define rules to archive or delete objects after N days.

DELETE rules take precedence over ARCHIVE rules.

## Pre-Authenticated Requests

Provides a way to let users access a bucket or an object without having their own credentials

This is for private buckets.

The request can be:

- for an object or a bucket
- have a time limit
- allow R, W or R/W permissions

Or just use a Public bucket.

## Other features

- cross-region copy
  - copy objects to buckets in the same or other regions
  - currently objects must be copied 1 by 1 - no bulk copy
- re-authenticated requests
- lifecycle rules
- multipart upload
- strong consistency
  - the most recent copy of the data is always retrieved
- durability
  - stored redundantly on multiple storage servers in multiple ADs
- encryption - Data encrypted with AES-256
  - you can provide your own keys if you like

