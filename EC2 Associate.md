##### Elastic IPs:
 - IP that attaches to another instance on failover(bad practice compared to DNS or LB)
 - defaultly 5 per account
##### EC2 Placement Groups:
Groups for optimized physical placement within the DCs.
- Cluster - Close Racks for low latency and 10 Gbps Bandwidth
- Spread - On different physical hardware within AZ (Max 7 EC2s per AZ)
- Partitions - Partition Groups Dont share racks with other partitions.
  Can be used to make sure an app isnt located within one physical hardware(Findout where they are on metadata service)
  
##### EC2 Hibernate:
Saves RAM to root EBS before stop. On start, restores from snapshot instead of full boot --> faster startup, preserves process state.
- Root EBS + AMI must be encrypted
- RAM < 150 GiB
- Not BareMetal