### DynamoDB Introduction

* Fully managed NoSQL database service 
* Single-digit millisecond response at any scale 
* Document and key/value models
* Mobile, gaming, ad-tech, IoT, live online voting, session management
* Store S3 object metadata
* Fast and predictable performance with seamless scalability. 
* No practical limit on table size, no constraints on number of items or bytes
* SSD storage
* Fully resilient and highly available
* This allows single-digit millisecond response at any scale
* 3 geographically distinct data centers - 3 facilities, not necessarily 3 AZs
* Data accessed via HTTPS endpoint, hardware & data center failures transparent to the application
* Performance scales in a linear way
* Fully integrated with IAM (including Federated Access and granualr and web identity)
* Eventually consistent reads (Default) - usually w/in a second (best read performance)
* Strongly consistent reads - reflects all writes that received a successful response prior to the read
* Read units - per 50 units
* Write units - per 10 units
* $0.25 per gig after first gig?
* Reserved capacity pricing option available
* Tables, items, attributes
* Fully integrated with IAM - including federated and Web identity (perfect for mobile and web app usage)

* DynamoDB is a collection of tables in each region
  * Service namespace is at region level, AZs unimportant in DynamoDB architecture
  * **NOTE** - you can NOT select a specific AZ when setting up a DynamoDB table!
  * Tables highest-level structure, at this level performance controlled and managed
  * Specify capacity units - minimum that is used on an operation:
    * Read capacity units (RCU) (4kb)  to a table
    * Write capacity unit (1kb) per second to a table
  * Supports eventually consistent reads - reads only acknowledged when at least 2 locations have responded with confirmed write as this is a distributed database
  * Reads by default take just from one region - means a read may not show a recent write if it's eventually consistent
    * Eventually consistent (default, use ½ unit per 4kb block) 
    * or strongly consistent (use 1 read unit per 4kb block)
* Billing is done based on the size of the data and the number of RCU and WCUs
* DynamoDB uses the performance and the data quality to manager underlying resource provisioning
* Think of partitions as an underlying server that can cope with a certain level of RCUs, WCUs, and store a certain amount of data

* Unlike SQL databases, the data structure or schema is NOT defined at the table level

#### Data Structures Within a Table

* **Row** = **Item** - each item can have different attributes, and different number of attributes
  * Row can have a different number of elements, or different elements altogether

![](DynamoDBTable.png)
* **Partition key / Hash key** - has to be unique w/in a table
  * Used to uniquely identify item in table
  * Used during QUERY operation to pull distinct item

* **Sort key / range key** 
  - allows one-to-many relationships for partition keys
  - returns sorted items (datetime)
  - can return a range of items based on the sort key

* Attribute types

    * String
    * Number
    * Binary
    * Boolean
    * Null

  * Dynamo Specific items
     * Document (List/Map): JSON
    * Set (Array)

* Can *copy* directly from DynamoDB to Redshift using COPY command in Redshift

* On EMR , DynamoDB is integrated with Apache Hive - can read and write data in DynamoDB tables - allows you to query live DynamoDB with SQL-like language

* Can copy DynamoDB table data to Bucket in S3 (and vice versa)

* Can copy DynamoDB table data to HDFS (and vice versa)

* Perform join operations on DynamoDB tables

* **Data Pipeline** - used to import/export DynamoDB table data to/from S3

    * Data Pipeline launches EMR, which reads/writes to/from DynamoDB and writes to S3 bucket  (export)or DynamoDB table (import)

* **EC2** - can use apps to read/write to/from DynamoDB

* **Lambda** - can create triggers that automatically respond to events in DynamoDB streams
  * Triggers can be used to react to data modifications in DynamoDB tables

* **Kinesis Streams** - using Kinesis Client Library and Kinesis Connector Library, can consume from Kinesis Streams and emit to DynamoDB

---


* [Back: Glacier (4:02)](Glacier.md)
* [Next: DynamoDB Partitions (11:16)](DynamoDB_Partitions.md)
