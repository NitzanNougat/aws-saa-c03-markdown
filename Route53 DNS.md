Zones contain records for that zone. A record like `my` in the zone `example.com` resolves to `my.example.com`.  
The apex record is the root of the zone (e.g., `example.com`).
private zones must be associated with a VPC

~~DNSSEC - add?~~

Each record includes:
- Record name (e.g., `my`)
- Record type (e.g., A, CNAME,NS)
- Value (e.g., IP address or hostname)
- Routing policy (how Route 53 responds to queries)
- TTL: Caching duration. Lower TTL speeds up propagation.
##### DNS Record Types:
- **A / AAAA:** hostname to single or multiple IPv4 / IPv6
- **CNAME:** hostname to hostname, not valid for apex records
- **Alias**(r53 only)**:** hostname to AWS resources:(supports apex)
	e.g. ELB and same zone records, but EC2 DNS doesn't work
- **NS:** delegates a zone to name servers
- **TXT:** used for domain ownership validation (e.g., certs via ACM)
	Example: ACM asks to create a TXT record with `"myvalue"`, if the query matches it confirms you own the domain
- **PTR:** IP to hostname (reverse lookup)
- **MX:** mail domain to mail server hostname + priority(for many MX records )
  
##### Health Checks:
Health checkers are public, so they can't access private endpoints.

**Endpoint Health Check**
- Uses 15 global health checkers (region configurable)
- Healthy/unhealthy threshold is 3 by default
- Considered healthy if 18% of checkers report it healthy
- Passes only on 2xx/3xx status codes
- Response body beginning text can be used to determine health
  
**Calculated Health Check**
- Combines results of up to 256 other health check
  
**CloudWatch Alarm Health Check:**
Use case: for private zones, create a health check that watches an alarm for private endpoints

##### Routing Policies:
Records with the same name and type must use the same policy.
Route 53 uses that policy to choose which record from the set to return for a query to that name and type.
All non simple policies optionally skip unhealthy targets via health checks
- **Simple:** one record, standard DNS response
- **Weighted:** split traffic by weight
- **Latency:** choose the lowest-latency target based on requester location
- **Failover**: uses a primary and secondary record. The primary must have a health check. If it fails, Route 53 uses the secondary if it is healthy. Both can be alias records to apply a separate policy.
- Geoproximity Routing: Each record has a bias(-99 to 99) to the size of the geoproximity area
- IP-based Routing: matches the client IP against a named list of CIDR blocks  
	Example: route users from a specific ISP to a dedicated endpoint
- Multi Value: return up to 8 healthy records; if more, 8 are picked randomly
  
##### R53 Interoperability:
Route 53 handles **domain registration** and **DNS hosting**, it can do both or just one.  
When hosting a domain, Route 53 allocates 4 name servers (NS) which you can provide to a third-party registrar.
