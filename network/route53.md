## DNS

### Types of Records:

- NS Records (Name server records)
- SOA Records (Start of Authority)
- A Records (Address): translates domain to address
- Alias Records: similar to CNAME, maps domain names to Load Balancers, CloudFront or S3 buckets; this is useful as IP addresses of Load Balancers may change
- MX records (Mail Server Records)
- CNAME (Canocical Name Records): resolves one domain to another, AWS charges per DNS call to CNAMEs
  - TTL - how long DNS records are cached

### Routing Policies:
- Simple: default routing policy when a record set is created. Used for forwarded traffic from a domain to a single resource.
- Weighted: Traffic can be set to be split between resources, e.g. 80% and 20% for two load balancers that resolve traffic to the same web address
- Latency Routing Policy: AWS selects the resources that has the lowest latency
- Failover: used when there is an active and passive sites setup. If the healthcheck fails traffic is routed to the healthy instance on passive route. Record set needs to be associated with a HealthCheck that was created earlier.
  - Do this as an example
