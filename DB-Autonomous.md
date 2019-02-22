# Autonomous Data Warehouse  (ADW)

- Columnar Format
  - All tables use HCC
- Creates Data Summaries
- Memory Speeds Joins, Aggregates
- Statistics updated in real-time while preventing plan regressions
- Automatic Backups
  - 60 day retention
  - manual backups are not required for normal operation

# Autonomous Transaction Processing (ATP)

- Row Format
- Automatically Creates Indexes
    - 19c+
- Memory for Caching to Avoid IO
- Statistics updated in real-time while preventing plan regressions  

Six Questions to Provision ATP

- Compartment?
- Display Name?
- Database Name?
- Number of CPUs?
- How many TB?
- Admin Password?

# Data Loading

Data Sources
Any supported ORACLE_LOADER format

- OCI Object Storage
- OCI Object Storage Classic
- AWS S3
- Azure

## Small Data Load

- SQL Loader
- Scripts that insert data

## Large Data Load

- Stage in OCI Object Storage
- Load with new PL/SQL API for loading data
  - DBMS_CLOUD and DBMS_CLOUD_ADMIN
  - [DBMS Cloud Packages](https://docs.oracle.com/en/cloud/paas/autonomous-data-warehouse-cloud/user/dbmscloud-reference.html)

OCI Object storage requires creating a credential using a _Swift_ password.

Apparently the _Swift_ password is from OpenStack Object Storage component _Swift_.

(I do not yet know anything about Swift)

Create Credential:

```sql
begin
dbms_cloud.create_credential(
  credential_name => 'OBJ_STORE_CRED',
  username => 'tenant1',
  password => ’password'
);
end;
/
```

Load Data:

```sql
begin
dbms_cloud.copy_data(
  table_name =>'CHANNELS',
  credential_name =>'OBJ_STORE_CRED',
  file_uri_list =>'https://swiftobjectstorage.us-ashburn-1.oraclecloud.com/v1/dwcsdemo/DEMO_DATA/chan_v3.dat',
  format => json_object(
    'ignoremissingcolumns' value 'true',
    'removequotes' value 'true'
    )
);
end;
/
```

Monitor Data Load:

```sql
select table_name,status,rows_loaded,logfile_table,badfile_table
from user_load_operations;
TABLE_NAME STATUS ROWS_LOADED LOGFILE_TABLE BADFILE_TABLE
-------------------- --------- ----------- -------------------- --------------------
CHANNELS FAILED COPY$1_LOG COPY$1_BAD
CHANNELS COMPLETED 5 COPY$2_LOG COPY$2_BAD
```

# REST API

Many operations can be performed via REST

[Autonomous REST API](https://docs.cloud.oracle.com/iaas/api/#/en/database/20160918/AutonomousDatabase/ "Autonomous REST API")

# Users

- create user identified by Some#C0mplexPa55word!
- grant the DWROLE role for std user/developer
