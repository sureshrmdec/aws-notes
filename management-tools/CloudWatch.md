#### Monitoring of EC2, EBS, S3 metrics
- Can notify when thresholds are reach AND stop or terminate servers (e.g. they have not been used frequently)

#### Metric Granularity:
- Standard Monitoring - 5 mins
- Detailed Monitoring - 1 mins (minimum granularity)

#### CloudWatch Alarms:
- Can monitor any AWS CloudWatch metric, including charges on AWS bills

#### Status Check Types:
1. System Status Check (checks the underlying physical host):
    - loss of network connectivity, system power, software issues on the physical host, hardware issues
    - Resolve issues by stopping then starting the VM (starts on a different physical host)
2. Instance Status Check (checks the virtual machine):
    - failed system status checks, misconfigured networking or startup configuration, corrupted file system, incompatible kernel
    - Solution: reboot the instance or make modifications to the operating system

#### EC2 Status Checks:
* RAM not monitored by default
- [Monitoring Script Installation]("https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/mon-scripts.html"):
    - Install Perl dependencies 
    - Download Perl CloudWatch script
    - Run the verification script to ensure instance can communicate with CloudWatch
    - Run the script with arguments for memory utilisation reportinghttps://docs.aws.amazon.com/AWSEC2/latest/UserGuide/mon-scripts.html
    - Add this command to crontab for automated monitoring

#### EBS Volume Status Checks:
- ok (normal)
- warning (degraded/severly degraded - performance is below/well below expectations)
- impaired (volume performance is severly impacted)
- insufficient data (no data is obtained from volume)

#### ELB Status Checks:
- only reports on metrics when the load balancer has requests
- monitored every 60 seconds
- Includes HealthyHostCount, RequestCount, Server errors etc
- SurgeQueueLength: count of the total number of requests that are pending submission to a registered instance
- SpilloverCount: count of the total number of requests that were rejected due to the queue being full

#### Monitoring Elasticache:
CPU Utilisation:
- Memcache: multithreaded, can handle loads of up to 90%. More nodes will need to be added if 90% CPU Utilisation is exceeded. 
- Redis: not multithreaded. To determine the point in which to scale, take 90 and divide by the number of cores
Swap Usage:
- Amount of disk storage space reserved on disk if computer runs out of RAM. Typically Swap size is equal the RAM capacity size
- Memcache should not exceed 50Mb Swap Usage. If 50Mb is exceeded then memcache_connections_overhead parameter will be flagged.
Evictions:
- Old item removed for new item. Eviction threshold should be based off the application
- Memcached options: scale up (add memory to existing nodes) or scale out (add more nodes)
- Redis options: only scale out (add read replicas)
Concurrent Connections: 
- If large increase in number of concurrent connections is noted this means that there is a large traffic spike or application is not releasing connections 

#### RDS Monitoring:
- RDS Metrics can be monitored and events can be triggered using CloudWatch RDS Metrics 
- Important Metrics:
    - DatabaseConnections (number of connections to RDS instance)
    - DiskQueueDepth (Number of read or write I/O operations queue to RDS, preferrably this should be 0)
    - FreeStorageSpace ()
    - ReplicaLag (measured in seconds, the time difference between read replicas)
    - ReadIOPS, WriteIOPS, ReadLatency, WriteLatency

Dashboards
- Alarms - allows you to set alarms that notify you when particular thresholds are hit
- Events - CloudWatch events helps you to respond to state changes in your AWS resources
- Logs - CloudWatch logs helps you aggregate, monitor and store logs
