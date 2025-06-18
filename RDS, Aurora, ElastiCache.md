### Amazon Relational Database Service(RDS):
Collection of managed Services to deploy operate and scale DBs like MySQL, PostgreSQL and MariaDB.

- ❌ “Database as a Service” 
- ✅ **DatabaseServer-as-a-Service**
  
  
**Pros:**
- Automated provisioning, OS patching
- Continuous backups and Point in time Restore
- Monitoring dashboards
- Read replicas for improved read performance
- Multi AZ setup for DR
- Maintenance windows for upgrades
- Scaling capability
- Storage backed by EBS
**Cons:**
- Cant ssh into instances

#### Backups and Restores

**Automated backups:**
- Daily Snapshots
- Transaction logs : Every 5m(PITR)
- Retention: 0-35d (Defaultly 7d)
- Backup window: HH:MM
  
**Manuel Snapshots:** No automatic deletion

#### Scaling:
- Compute scaling is Manuel
##### Storage Auto Scaling
- Triggers if usage >90% for 5m, and 6h since last scale
- Set Max Storage
##### Async Read Replicas:
- Up to 15 replicas, Each has unique connection string
- Paid cross region replication
- Can be converted to a standalone DB or Secondary(Sync) for Multi AZ.
#### Multi AZ(DR)
- Secondary DB in different AZ with sync replication.
- One DNS and automatic failover in case of AZ failure.
  
#### RDS Custom:
- Oracle and Microsoft SQL only.
- SSH access enables manual patching and config changes.
- Stop automation mode before changes that conflict with automation
  
### Amazon Aurora:
Cloud optimized manged service suppoting **MySQL** and **PostgreSQL**

##### Storage Architecture
Aurora uses a Shared Cluster Volume with 6 copies across 3 AZs
- 4/6 Available copies needed for writes, 3/6 for reads
- self healing with peer-to-peer replication
  
##### Cluster Architecture:
- Master + up to 15 Aurora Read Replicas
- Automated master failover < 30s
- Writer endpoint --> Current master
- Reader Endpoint --> Load balancing for all read replicas
- Custom Endpoint --> Load balancing for **chosen** read replica/s

##### Scaling:
- Storage auto scaling 10GB - 128TB
- Read replicas horizontal auto scaling:
	  It chooses the new instance size according to Aurora Scaling Policies
- Compute scaling is Manuel
##### Aurora Serverless:
- Auto-Scaling with min/max units.
- Billing per-second
- Same resilience as Aurora (6 copies across AZs)
  
##### Global Aurora:
**Aurora Global DB**:
- Storage based async cross-region lag < 1s  --> good for low latency reads
- 1 primary (r/w), up to 5 secondary (ro) regions, each with up to 16 replicas
- Region promote RTO <1m

**Aurora Cross Region Read Replicas:**
SQL-based async, longer cross-region lag → good for DR, not reads (stale data)
##### Backups:
- Retention 1–35d (mandatory)
- 0 RPO, PITR with 1s granularity within retention
  
##### Aurora Database Cloning:
- Faster than snapshot & restore
- Uses copy-on-write protocol:
	- Initially, the new DB cluster uses the same data
	  volume as the original DB cluster
	- When updates are made to the new DB cluster
	  data, then additional storage is allocated and data is
	  copied to be separated

##### RDS & Aurora Security:
- **At-rest encryption:**
	- KMS encryption is set at launch and must be the same for master and replicas.
	- To encrypt later snapshot and restore with encryption
- **At-transit:** TLS by default,  AWS TLS root certificates
- IAM roles optionally instead of user/pw
- Network access controlled by SGs and VPC
- No SSH unless using RDS Custom
- Audit logs can go to CloudWatch for longer retention

##### Amazon RDS & Aurora Proxy:
- Managed, serverless proxy for RDS and Aurora
- Pools connections to reduce load, timeouts, and failover time
- Uses IAM auth, stores creds in Secrets Manager
- VPC-only access
- Supports Aurora, MySQL, Postgres, MariaDB, SQL Server

##### Aurora Machine Learning:
- Enables ML predictions to apps via SQL
- Integrates with SageMaker and Comprehend (sentiment analysis)
- No ML experience needed
- Use cases: recommendations ,ads 
  
##### Babelfish for Aurora PostgreSQL:
Allows to run MS SQL Server queries  by translating T-SQL

##### ElastiCache:
Managed Redis/Memcached in-memory DBs
involves heavy application code changes(caching logic)


##### Redis vs Memcached:
**Redis:**
• Multi AZ with Auto-Failover
• Read Replicas
• Backup and restore
• Sets and Sorted Sets

**Memcached**:
• Multi-node for sharding
• Non persistent
• Multi-threaded

##### ElastiCache Security:
- Network access via SGs and VPC
- Encryption set at launch: in-transit (TLS), at-rest (KMS)
**Redis:**
- Supports IAM auth or Redis AUTH (user/token)
  
##### ElastiCache Patterns:
- **Lazy loading:** update cache on DB reads, risk of stale data
- **Write-through:** update cache on DB write, no stale data
- **Session store:** cache session state with TTL
