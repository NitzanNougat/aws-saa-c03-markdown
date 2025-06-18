## Elastic Load Balancing(ELB)
==Format this into non list==
- single-point of contact, distribute seamlessly across downstream instances.
- Types
    - Classic Load Balancer(depracted)
    - Application Load Balancer(L7)
		- Target groups like:
            - Private IP
            - EC2
            - Lambda Function
            - ECS Task
		 - Proctocols: HTTP/S ad Websocket
		 - Client IP Saved inside header
		 - Health checks are per Target group
	    
    - Network Load Balancer(L4)
        - Fast Traffic Over TCP/UDP
        - Supports TCP/UDP Over TLS
        - Static IP per AZ
	    - Target Groups: Private IPs and ALB.
	    - Health Checks support TCP, HTTP/S 
    - Gateway Load Balancer(L3)
	    - Target groups of Virtual Appliances(like FW)
#### ELB Options:
##### Sticky Sessions:
Uses cookies to keep client on same target.
- Durability cookies: Time based sticky session
	- AWSELB/AWSALB
 - Application cookies: Managed the app logic
		- AWSALBAPP
		- Custom cookie name
		  
		  
##### Cross-Zone Load Balancing:
- ALB: Enabled by default (can be disabled at the Target Group level), free
- NLB & GLB: Disabled by default, paid
- CLB: Disabled by default, free


##### SSL Certificates:
- **CLB:** Max 1 cert
- **NLB & ALB:** Multiple certs via SNI (Server Name Indication), which specifies the target server name during TLS handshake, enabling the load balancer to select the appropriate certificate for each request.

##### Deregistration Delay(ALB,NLB) / Connection Draining(CLB):
Time to complete requests before removing target., 1-3600 seconds (default: 300).

==Maybe add data for Routing rules==

### Auto Scaling Group(ASG)
An Logical group for EC2s with the same conifguration with automatic scaling and self-healing
Attributes:
- Launch template:
	- AMI + Instance Type
	- EBS Volumes
	- Security Groups
	- SSH Key Pair
	- IAM
	- Networking
	- User Data
- Min/Max Size
- Scaling Policies:
	- **Target tracking**: scale to maintain a specific metric like CPU=60%
    - **Step scaling**: change capacity in steps based on alarm thresholds.
    - **Scheduled Scaling**
    - Predictive scaling
- Scaling Cooldowns: Default 300s
  
  
  
==Maybe Add data to ASG  how does the it work in detail==