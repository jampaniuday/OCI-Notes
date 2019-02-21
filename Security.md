# Security

## Overview

Data is _always_ encrypted in OCI.

However you can create and use your own keys for further protection.

- Keys are stored in Vaults
- Vaults should be in their own compartment
  
Sample policies for using and managing vaults and keys

- Vaults created in compartment VaultCompartment
- VaultAdministrators
  - manage vaults
- KeyAdministrators
  - manage keys
  - use vaults

[KMS FAQ - Key Management Service](https://cloud.oracle.com/cloud-security/kms/faq "KMS - Key Management Service")

### Sample Policy rules

Allow Groups

- allow group VaultAdministrators to manage vaults in compartment VaultCompartment 
- allow group KeyAdministrators to manage keys in compartment VaultCompartment
- allow group KeyAdministrators to use vaults in compartment VaultCompartment

Allow Services

- allow service objectstorage-us-phoenix-1 to manage keys in compartment VaultCompartment
- allow service blockstorage to manage keys in compartment VaultCompartment

## Key Management

Features
- Centralized key management capabilities via HSM
- Highly available, durable, and secure key storage
- Integration with select Oracle Cloud Infrastructure services

### HSM

Hardware device dedicated to key management

[Hardware Security Module](https://en.wikipedia.org/wiki/Hardware_security_module "Hardware Security Module")

- HSMs meet Federal Information Processing Standards (FIPS) 140-2 Security Level 3 security certification. 
- tamper-evident
- physical safeguards for tamper-resistance
- requires identity-based authentication
- deletes keys from the device when it detects tampering

### Keys

The keys used are specific to OCI

- keys cannot be imported
- keys cannot be exported
- keys can be rotated
- keys cannot be deleted
- keys can be disabled

### Key Rotation

Keys may be rotated at any time.

Keys always retain the same OCID.  

Rotating the key creates a new version number of the key with the same OCID.

Existing data remains encrypted with the previous version.

The old version is retained to decrypt already encrypted data.

New Data is encrypted with the new version of the key.

Existing data is re-encrypted only when modified.

### Vault

Keys are organized in to _Vaults_

- Vaults can be deleted
  - doing so requires a waiting period
  - deleted Vaults cannot be recovered
  - deleting a Vault can render data unreadable

