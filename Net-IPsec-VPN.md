# IPsec VPN 

The OCI VPN 

## Components

- VCN: Virtual Cloud Network
- DRG: Dynamic Routing Gateway
- CPE: Customer Premises Equipment (created as object in OCI)

## Workflow

- Create a Virtual Cloud Network (VCN)
- Create a Dynamic Routing Gateway (DRG)
- Attach DRG to your VCN
- Update VCN Router to route traffic to DRG 
- Create a CPE Object and add on-premises router Public IP address
- From DRG, Create an IPsec Connection between CPE and DRG and provide a Static Route
- Configure on-premises CPE Router