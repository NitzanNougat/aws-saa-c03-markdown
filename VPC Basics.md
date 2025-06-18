###### VPCs:
- **VPCs are within 1 account & 1 region**
- Subnets are within 1 AZ.
- Both Cannot be transferred two another az and region
- No Peering by default
  
###### Default VPC:
- Bad practice
- **IP range: 172.31.0.0/16** 

##### Firewall Rules Types:
**Security Groups:**
- Stateful
- Deny By Default( only allow rules)
- VPC Scoped, Attached To EC2
- Instances can have multiple SGs
- Cause Time Out
- Source and Dest types:
	- CIDRs
	- Other SGs
	- Prefix Lists(Like SaaS IP lists)
	- AWS Services

- **NACL: Network Access Control List**
    - Stateless
    - VPC Scoped. attach to subnets
    - Deny By Default
    - Allow and deny rules with priority
    - Subnets are always attached to a **single** NACL (Default Nacl is allow all)
    - Only allow CIDR as destination

ENIs(NICs):
- AZ Scoped and bound
- primary (private) IPv4 + secondary IPv4
- Movable between EC2s
- 1 x EIP per private IPv4

