### Database AWS Concepts


#### Types of Reads:

1. Eventual Consistent Reads:
  -
  ### Types

  - RDS - OLTP:
    - SQL
    - MySQL
    - PostgreSQL
    - Oracle
    - Aurora
    - MariaDB
  - DynamoDB - NoSQL
  - RedShift - OLAP
  - Elasticache - In Memory Caching:
    - Memcached
    - Redis


  ### Automated Backup Types

  There are two different types: automated backups and database snapshots
  1.Automated backups:
  - Automated backups allow you to recover your database to any point in time within a retention period.
  - Retention period is 1 - 35 days.
  2.Snapshots:
  - Snapshots taken daily that also store transaction logs throughout the days
  - when a recovery is performed AWS will choose the most recent backup and apply the transaction logs from that days. This allows for very granular backups

  ### Database Patterns

  - Multi AZ RDS
  ![RDS](./pictures/db-multi-az-rds.png )

  - Read Replica
  ![RDS](./pictures/db-read-replica.png )
  * allow for read only copy of production database, achieved via async replication from primary RDS to the read replicas. Use for heavy read workloads
  * no multi AZ read replicas
