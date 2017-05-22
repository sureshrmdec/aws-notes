SA exam tips:

1.
US STANDARD is a redundant term. The AWS exams still use the term, so you need to be familiar with it. The questions is still valid just ignore the reference to US STANDARD and any past discrepancies that may have existed.
Further information:
https://forums.aws.amazon.com/ann.jspa?annID=3112
https://aws.amazon.com/s3/faqs/

2. If a EC2 instance on a private subnet cannot access the internet via a NAT instance disable the source/destination check on the NAT instance

3. Redshift block size for columnar storage: 1024KB

4.You have created a new subdomain for your popular website, and you need this subdomain to point to an Elastic Load Balancer using Route53. Which DNS record set should you create? CNAME

5. Amazon S3 provides ________. Unlimited storage
6. Which consistency model for PUTS of new objects does S3 offer? Read After Write Consistency
7. S3 has eventual consistency for which HTTP Methods? overwrite PUTS and DELETES
8. Due to international monetary regulations issued by the IMF, a large multi-national banking organization requires that all their Australian customers' data must not leave the Australian jurisdiction. Similarly, all Japanese customers' data may not leave the Japanese jurisdiction without explicit permission from the IMF. While registering, a user must include their residential address as part of their user profile. What steps should be taken to enforce these regulations on a web-based application running on EC2? ~Due to the strict regulations, you should use a third party data provider to verify the users location based on their profile. It would not be appropriate to rely on latency based routing, as this would not always be 100% accurate.~
9. You've been tasked with building a new application with a stateless web tier for a company that produces reuseable rocket parts. Which three services could you use to achieve this? RDS, DynamoDB, and ElastiCache
10. Your company has decided to set up a new AWS account for test and dev purposes. They already use AWS for production, but would like a new account dedicated for test and dev so as to not accidentally break the production environment. You launch an exact replica of your production environment using a CloudFormation template that your company uses in production. However, CloudFormation fails. You use the exact same CloudFormation template in production, so the failure is something to do with your new AWS account. The CloudFormation template is trying to launch 60 new EC2 instances in a single availability zone. After some research you discover that the problem is ________. For all new AWS accounts, there is a soft limit of 20 EC2 instances per region. You should submit the limit increase form and retry the template after your limit has been increased.
11. You need to add a route to your routing table that will allow connections to the internet from your subnet. Which of the following routes should you add? Destination: 0.0.0.0/0 --> Target: your Internet gateway
12. What is the maximum VisibilityTimeout of an SQS message in a FIFO queue? 12 hours
13. The valid ways of encrypting data on S3 are Server Side Encryption (SSE)-S3, SSE-C, SSE-KMS or a client library such as Amazon S3 Encryption Client.
14. How long can a message be retained in an SQS Queue? 14 days
15. In RDS, what is the maximum size for a Microsoft SQL Server DB with SQL Server Express edition? 10GB
16. How many regions? 16 regions
