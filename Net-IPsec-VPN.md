# IPsec VPN 

The OCI VPN 

## Components

- VCN: Virtual Cloud Network
- DRG: Dynamic Routing Gateway
- CPE: Customer Premises Equipment (created as object in OCI)
  - 2 or more are required

## Workflow

- Create a Virtual Cloud Network (VCN)
- Create a Dynamic Routing Gateway (DRG)
- Attach DRG to your VCN
- Update VCN Routing Table to route traffic to DRG 
- Create a CPE Object and add on-premises router Public IP address
- From DRG, Create an IPsec Connection between CPE and DRG and provide a Static Route
  - OCI Creates redundant tunnels in different ADs that are logically and physically separate
  - This is for HA
- Configure on-premises CPE Router
  - 2 or more are required