## DynamoDB

a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. Fully managed and supports both document and key-value datamodels. Great for mobile, web, gaming, ad-tech and IoT
- Stored on SSD storage
- Spread across 3 geographically distinct datacentres
Two types of reads:
- eventual consistent reads:
  + consistency across all copies of data generally reached with a 1 second
- strongly consistent reads:
  + returns a results that reflects all writes that received a successful response prior to the read.