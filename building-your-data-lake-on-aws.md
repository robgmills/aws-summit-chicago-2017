# [Building Your Data Lake on AWS](https://awschicago17.smarteventscloud.com/connect/sessionDetail.ww?SESSION_ID=123335)

## Abstract
Increasing demands to collect, store, and analyze massive amounts of data often means that the same tools and approaches that worked in the past, don't work anymore. That's why many organizations are shifting to a data lake architecture. A data lake is an architectural approach that allows you to store massive amounts of data into a central location, so it's readily available to be categorized, processed, analyzed and consumed by diverse groups within an organization. In this tech talk,
we introduce key concepts for a data lake and present aspects related to its implementation. We highlight the core components of a data lake, such as storage, compute, analytics, databases, stream processing, data management, and security. We discuss how to choose the right technologies for each component of the data lake, based on criteria such as data structure, query latency, cost, request rate, item size, data volume, durability, and so on. We also provide a reference architecture
and recommendations to get started with a data lake implementation on AWS. Learning Objectives:

Understand key concepts and architectural components of a data lake architecture
Describe how and when to use a broad set of analytic and data management tools in a data lake architecture
Get insights on how to get started with a data lake implementation

## Notes

Ben Snively, Senior Solutions Architect, AWS

### Agenda

0. What is a data lake?
0. How are others building a data lake?

### What is a Data Lake?
* An _architectural approach_ that allows you to store massive amounts of "raw" data into a central location
* It's _readily available_ to be _categorieze, processed, analyzed, and consumed_ by _diverse groups_.
* "schema on read"
* make data available to diverse groups of users
    * data scientists
    * BI/BA
    * application and operation teams (log analysis)
* picking the right tool is important and depends on your use case

### Why use a Data Lake?
* Leverage all data within your organization

### Cloud architecture evolution
* virtualized -> managed -> serverless
* virtualized unit of scale === "server"
* managed unit of scale === "platforms"/"solutions"
    * still thinking about servers, but managed on your behalf by provider
* serverless unit of scale === "?"

### Challenges with legacy data architectures
* Can't move data across silos
* Can't handle semi-structured or unstructured data
* Can't deal with dynamic data and real-time processing
* Complex ETL processes
* Difficulty applying consistent data governance across all data sets

Legacy adoption either
* migrate data into a solution (fit data to tool)
* use the solution that best matches where/how your data is stored (fit tool to data)

### Legacy data architectures exist as isolated data silos
Hadoop |  ?????? | SQL

### Navigating the data lake
?????

### Centralized data, single source of truth
Why is the data distributed in many locations?  Where is the source of truth?

### Quick ingest
How can I collect data quickly from various sources and store it efficiently?
Quickly ingest data without needing to force it into a predefined schema

Don't need to go through a data modeling exercise for every new data source

### Data Lakes on AWS
#### Why AWS?
Implementing a Data Lake architecture requires a broad set of tools and technologies to serve an increasingly diverse set of applications and use cases.

Picking the right tool for the right job, on a consumption-based model

#### AWS services for data lake
* Ingestion to S3
    * Kinesis Firehose - real time queues
    * Database Migration Service - take data in a database form and put it in S3
    * Snowball/Snowmobile - physical device sent to customer
    * Direct Connect
* Catalog
    * DynamoDB
    * Elasticsearch Service
* Processing and Analytics
    * Athena - SQL interface on top of S3 data
    * Kinesis - Real time analytics
    * Redshift - data warehouse
    * QuickSight
    * EMR - Hadoop as a Service (Pig, Hive, Spark)
    * RDS
    * Elasticsearch Service

#### Data Lake reference architecture

Fine grained access control with IAM using prefixes
Share data and have it billed back to data owner.

KMS == key management service, encryption keys.

### S3 - Center of the Data Lake
#### Benefits of an AWS data lake
* decouple storage and compute by making S3 object-based storage
    * performance not really a concern (see blog posts by Netflix et al)
* consolidate and centrally manage and govern your data
* flexibility to use any and all tools in the ecosystem.  The right tool for the job.
* Future proof your architecture.  As new use cases and new tools emerge, you can plug and play current best of breed.

#### Why Amazon S3 for Data Lake?
* Durable - 11 9s of durability
* Available - Design for 99.99% availability
* High performance - Multiple upload, range GET
* Easy to use
    * REST API
    * AWS SDK
    * Read-after-create consistency
    * event notification
    * lifecycle policies
* Scalable
    * store as much as you need

#### Implement the right cloud security controls
* Encryption
* Security
    * IAM 
    * bucket policies
    * ACLs
* Compliance
    * Access logs
    * lifecycle management policies
    * ACLS
    * versioning

### Process and analyze
#### EMR
* Hadoop/HDFS clusters
* Hive, pig, impala, Hbase, sparke, presto
* Easy to use, fully managed
* On demand, reserved instance and spot pricing
* Tight integration with S3, dynamoDB, and Kinesis

#### Choose your instance types
* Batch Process
    * m1, m3 family
    * general
* Machine learning
    * c3 family
    * cc1.4xlarge, cc2.8xlarge
    * cpu
* spark and interactive
    * memory
    * m2 family
    * r3 family

Can be resized using autoscaling or ....

#### Easy-to-use Spot instances
* Standard pricing for on demand capacity
* up to 86% lower on average off on demand pricing

Scale for predictable SLA costs, but augment with spot instances to improve performance out of cluster

#### Interactive Query Service
* Amazon Athena
* query directly from S3
* Use ANSI SQL
* Serverless
* Multiple data formats
* Pay per query

#### DynamoDB
* NoSQL database
* Seamless  scalability
* zero admin
* single digit millisecond latency

#### Redshift
* data warehouse
* BI/BA use cases
* SSL to secure data in transit
* encrption to secure data at rest
* no direct access to compute nodes
* audit logging, cloudtrail, KMS integration
* VPC support
* Queries hit leader node, leader node farms out to compute nodes, compute nodes read data off of S3/DynamoDB

#### Redshift Spectrume
* data catalog points to data in the data lake
* query in redshift against random data sets in S3

#### Elasticsearch Service
Common use cases
* logs to s3, load in ES
* traditional search

#### Kinesis
a portfolio of services, not a single service
* streams
    * for technical developers
    * build custom applications that process or analyze streaming data
    * 1 shard === 1K records/second, easy to ramp up or down to fit capacity
* firehose
    * for all developers, data scientists
    * easily load massive volumes of streaming data into S3, redshift, etc
* Analytics
    * For all developers, data scientists
    * easily analyze data streams using standard SQL queries

https://aws.amazon.com/kinesis/analytics/
https://github.com/scopely/kinesis-vcr

#### Amazon AI

https://aws.amazon.com/amazon-ai/





















