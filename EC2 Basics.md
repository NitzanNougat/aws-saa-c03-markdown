User Data: Post Provisioning Script
Pub-IP: Changes Post Restart If it is auto assigned

Instance Types:
Example: `c7g.xlarge`

Breakdown:
- `c` → **Compute optimized** family
- `7` → **Generation 7**
- `g` → **Graviton processor (ARM-based)**
- `.` → delimiter
- `xlarge` → **Instance size** 

- VPC networking by default
- Local on-host storage or **EBS**
##### Instance Lifecycle
- Running
- Stopped
- Terminated
  
##### Connecting to EC2:
- Regular SSH / RDP
- EC2 Instance Connect

**EC2 Purchasing Options:**
- On Demand:
	- Per Second Billing
- Reserved:
	- Reserve specific: instance type, region, tenancy, OS
	- Period: 1yr (+) or 3yr (+++)
    - Payment: no upfront (+), partial (++), upfront (+++)
    - Scope: Regional or Zonal (reserves AZ capacity)
- Saving Plan:
	- Commit to e.g - 10$ per hour for 1 year
	- Usage Beyond it    
Other EC2 Costs:
- EBS billed also when stopped.
  
