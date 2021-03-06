## DynamoDB Overview
- Flexible NoSQL database service
- Single-digit millisecond latency at any scale.
- Fully managed and supports both document and key-value data models.
- Ideal for mobile, web, gaming, ad-tech and IoT
- Stored on SSD storage
- Spread across 3 geographically distinct data centres

### Types of Reads
- Eventual Consistent Reads:
  + consistency across all copies of data in data centres generally reached with a 1 second
- Strongly Consistent Reads:
  + returns a results that reflects all writes that received a successful response prior to the read.
  + read performance not as good as eventual consistent reads

### Structure Terminology
- Table: collection of key-value stores
- Item: an individual unit in a collection, e.g. a student or product for sale
- Attribute: the key-value associated with an Item.

### Pricing
Provisioned Throughput Capacity:
  - Write throughput $0.0065 per hour for every 10 units
  - Read throughput $0.0065 per hour for every 50 units
First 25GB stored per month is free
Storage costs of $0.25GB per month there after

TODO: Examples
103GB stored in a DB
Create tables using Nodejs script on Lambda or EC2

### Primary Keys
#### Single Attribute Keys
Single attribute keys (similar to unique ID) are a Partition Keys (Hash Key) composed of only one attribute (e.g. User ID)

The Partition Key value is used as an input to a hash function. The output of the hash function determines the partition, or memory location where the data is stored.

#### Composite Attribute Keys
Composite attribute keys consist of a Partition Key and a Sort Key of two attributes (e.g. Hash and Range Key)

When a composite key is created it may have the same partition key as another item but it must have a different sort key, making no two composite keys alike. Items with the same partition key are stored together and the data stored at this location is sorted by sort key value.

### Indexes
Local Secondary Indices:
- Consist of an identical Partition or Hash Key, but a different sort key. Local Secondary indexes can only be generated when creating a table and cannot be modified after the table is made.

Global Secondary Indices:
- Global Secondary Indexes have a different Hash key and different sort key. This type of index can be created after table creation.

### Searching Items
- Query:
  Searches for Items in a Table using primary key attribute values to find a partition attribute name matching the search value.
  Optionally, a sort key attribute name and value, using a comparison operator can be used to query.

  Query results return all data attributes for items matching primary keys. `ProjectionExpression` parameter can be used so the Query only returns a subset of attributes.

  Results from a Query are always sorted by the sort key. For example. numeric data types are sorted in ascending order; strings are sorted by ASCII character code values. Reverse order of results from a Query can be enabled by using the `ScanIndexForward`

- Scan:
  A Scan returns all attributes and items in the table. A `ProjectionExpression` parameter can be used, similar to a Query, to return a subset of attributes of the items.

- Queries are more efficient in comparison to Scans.
- It is advisable to use Query, `Get` or `BatchGetItem` API functions instead for more efficient retrieval of desired information.

### Calculating Provision Throughput
- Calculating Read Provisioned Throughput:
  - All reads are rounded up in increments of 4KB
  - Eventually Consistent Reads consists of 2 reads per second
  - Strongly Consistent Reads consist of 1 read per second
  Read Throughput Calculation - ```
  Read Throughput = (Size of Read to the nearest 4KB / 4KB) * Number of Items
  ```
  - Divide the result by 2 for Eventually Consistent Reads
  Example: 120 units per minute; 5KB unites; Eventual Consistency used:
  ((8KB / 4KB) * (120 Items per Min / 60 seconds) / 2) = 1 Read Unit

- Calculating Write Provisioned Throughput:
  - All writes are 1KB
  - All writes consist of 1 write per second
  Write Throughput Calculation - ```
  Size of Write in KB * Writes Per Second
  ```

Errors concerning Provisioned Throughput:
 - 400 HTTP Status Code: `ProvisionedThroughputExceededException`
 - Maximum allowed provisioned throughput for a table or for one or more global secondary indexes has been exceeded  

### Web Identity Providers
Using the `AssumeRoleWithWebIdentity` API a user can authenticate with third parties like Facebook, Google and other Open-ID Connect-compatible Identity providers.

Web Identity Provider authentication process
1. Authenticate Identity provider (FB, Google etc)
2. Web Identity token return to users device
3. `AssumeRoleWithWebIdentity` Request made to AWS Security Token service
4. Temporary security credentials then provided to user (default 1 hour):
  - SubjectFromWebIdentity token provided by AWS STS allows user to access AWS resources

### Other
#### Batch Operations
If an application need to read multiple items, `BatchGetItem` API request can be used to retrieve up to 1MB of data, containing as many as 100 items. And this request can be used to retrieve multiple items from multiple tables.

#### Conditional Writes
DynamoDB can be written to at the same time by 2 or more users causing duplication of Items with differing values
Conditional writes can be used to prevent this by only allowing a write to occur when an Item's attribute is equal to a certain value. E.g. if old value = old value then up to new value. Conditional updates are idempotent operations.


#### Atomic Counters
- DynamoDB also supports atomic counters, where `UpdateItem` operation is used to increment or decrement the value of an existing attribute without interfering with other write requests. All write requests are applied in the order in which they were received. Atomic counters are not idempotent

#### DynamoDB Streams
DynamoDB Streams is a feature that captures any kind of modification of the DynamoDB tables, this includes taking images of states of an Item before and after modification. The images are stored for up to 24 hours and Streams is useful as an entry point for other functions performed on the data in the Stream.
