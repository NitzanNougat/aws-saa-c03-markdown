### EBS Basics: 
Network Block Storage that you can attach to EC2 as volumes.
- AZ scoped and bound
- Attached to one instance at a time
- Different physical storage types, different sizes, different performance profiles.
- Delete On EC2 Term: Defautly enabled on root vol.
- Snapshots & Volumes Can be auto-encrypted by KMS at rest and transit. 

### EBS Volume Types
EBS  Volumed are characterized in Size | Throughput | IOPS
##### General Purpose SSD(gp2/3)
- 1GB to 16 TB
-  Cost effective storage, low-latency
**gp3:** Can increase IOPS independently
**gp2:** 3 IOPS per GiB (size-dependent)

##### Provisioned IOPS SSD(io1/2)
- IOPS can be adjusted independently of size
- Consistent Low latency.
- Great for DBs
- Supports EBS Multi-attach: 
	- Attaches up to 16 EC2s
	- AZ Scoped 

io1: 
- 4 GiB - 16 TiB
- Max PIOPS: 32K/64K

io2 Block Express: 
- 4 GiB – 64 TiB
- Sub-millisecond latency
- Max PIOPS: 256,000

##### Hard Disk Drives (HDD)
• Cannot be a boot volume

st1: throughput Optimized HDD
sc1: archive HDD

##### Instance Store Volumes
Ephemeral Block storage attached Physically to EC2.

- Highest Performance
- Must attach at launch
- Included in instance price


### EFS - Managed NFS:
- Can be either Region or AZ Scoped
- Incompatible with windows
- Encryption at rest using KMS
##### Performance Mode(Set at creation)
- General Purpose (default): latency-sensitive use cases
- Max I/O: higher latency, throughput, highly parallel (big data, media processing)
##### Throughput Mode
- Bursting: throughput scales with size
- Provisioned: set your throughput regardless of storage size, ex: 1 GiB/s for 1 TB storage
- Elastic: scales throughput with usage
##### Amazon Machine Image (AMI):
An EC2 instance can be created from an AMI, or an EC2 can be used to create an AMI
- Regionally Scoped
- Contains
    - Permissions - who can and can’t use the AMI
        - Public - Everyone can launch instances from that AMI (Linux and Windows)
        - Owner - Implicit allow
        - Explicit - specific AWS accounts allowed
    - Boot Volume
        - The drive that boots the OS
    - Block Device Mapping
        - Links the volumes the AMI have
        - Mapping between volumes