---
id: 20230511170245
tags: [aws-saa-c03, big-data]
---

# Big Data

## The 3 V's of Big Data

* Volume - ranges from terabytes to petabytes of data
* Variety - includes data from a wide range of sources and formats
* Velocity - data needs to be collected, stored, processed, and analyzed
  within a short period of time

## Redshift

* Redshift is a fully managed, petabyte-scale data warehouse service,
  it's a large relational database used in big data applications
* Redshift can hold up to 16PB of data
* Redshift is relational, thus you can use standard SQL and business
  intelligence (BI) tools to query it
* Redshift is **not** a replacement for standard RDS databases
* Redshift is not HA, it can only be spun up in one AZ

## Elastic MapReduce (EMR)

* EMR is a managed big data platform that allows you to process vast
  amounts of data using open source tools, it's an ETL tool
* ETL - extract, transform, load
* It is simply a managed fleet of EC2 instances running open source
  tools
* EC2 rules apply you can use RIs and Spot instances

## Kinesis

* Kinesis allows you to ingest, process, and analyze real-time streaming
  data
* Kinesis Data Streams - used for real-time streaming for ingesting
  data, users are responsible for creating the consumer and scaling the
  stream
* Kinesis Data Firehose - near real-time data transfer tool to get
  information to S3, Redshift, Elasticsearch, or Splunk, it is easily
  integrated with AWS architecture
* Kinesis Data Analytics - analyze data using standard SQL, it is
  supported by both the above, it is a fully managed, serverless
  service
* If you need real time message delivery Kinesis is the best option
  (particularly over SQS)

## AWS Athena & AWS Glue

* Athena is a serverless service that simplifies analyzing data in S3
  using SQL, it removes the requirement of loading data into a database
* Glue is a serverless data integration service that makes it easy to
  run ETL workloads without having to manage any infrastructure
* Glue can design a schema for data making it easier to query with
  Athena

## QuickSight

* A fully managed BI data visualization service, used to create and
  share dashboards

## AWS Data Pipeline

* AWS Data Pipeline is a managed ETL service for automating the movement
  and transformation of data
* Overview:
  * Data driven - define data driven workflows
  * Parameters - define parameters for data transformations, service
    enforces the chosen logic
  * Highly available - hosted on HA, distributed infrastructure
  * Handling failures - automatically retries failed activities, can
    configure SNS notifications
  * AWS storage services - easily integrates with DynamoDB, RDS,
    Redshift, and S3
  * AWS compute - Utilised EC2 and EMR for compute requirements
* Components:
  * Pipeline definition - specify the business logic
  * Managed compute - service will create EC2 instances or use existing
    ones
  * Task runners - EC2 instances which poll for tasks and perform them
  * Data nodes - define the location and types of data to be inputted
    and outputted
* Use cases:
  * Processing data in EMR using Hadoop streaming
  * Importing or exporting DynamoDB data
  * Copying CSV files or data between S3 buckets
  * Exporting RDS data to S3
  * Copying data to Redshift

## Amazon Managed Streaming for Apache Kafka (MSK)

* Amazon MSK is a fully managed service for running applications that
  use Apache Kafka
* Provides control plane operations, modifies clusters as required
* Use Kafka data plane operations for producing and consuming data
* Open source versions of Apache Kafka support existing apps, tools, and
  plugins
* Components:
  * Broker nodes - specify the amount of broker nodes per AZ
  * ZooKeeper nodes - automatically created
  * Producers, consumers, and topics - Kafka data plane operations allow
    creation of topic and the ability to produce and consume data
  * Flexible cluster operations - perform cluster operations with the
    console, CLI, or APIs (SDK)
* Resiliency:
  * Automatic recovery - automatic detection and recovery from common
    failure scenarios
  * Detection - detection of broker failures result in mitigation or
    replacement of unhealthy nodes
  * Reduce data - tries to reuse storage from older brokers during
    failures to reduce data replication
  * Time required - impact time is limted to how long it takes MSK to
    complete detection and recovery (generally quite low)
  * After recovery - after recovery producers and consumers communicate
    with the same broker IP
* MSK Serverless offers automatic cluster management, fully compatible
  with Apache Kafka
* MSK Connect allows developers to easily stream data to and from Apache
  Kafka clusters
* Security and Logging:
  * Integrates with KMS for SSE requirements
  * Encryption at rest by default
  * TLS 1.2 for encryption in transit
  * Deliver broker logs to CloudWatch, S3, and Kinesis Data Firehose
  * Metics are sent to CloudWatch
  * All Amazon MSK API calls are logged to CloudTrail
* Push broker logs to CloudWatch, S3, or Kinesis Data Firehose

## Amazon OpenSearch Service

* OpenSearch is a managed service allowing you to run search and
  analytics engines for various use cases, succeeds Amazon Elasticsearch
  Service
* Features:
  * Quick analysis - quickly ingest, search and analyze data in
    clusters, commonly used in ETL processes
  * Scalable - easily scale cluster infrastructure
  * Security - Use IAM for access control, VPC SGs, encryption at rest
    and transit, and field-level security
  * Stability - multi AZ capable with automated snapshots
  * Flexible - has SQL support for BI apps
  * Integrations - easily integrated with CloudWatch, CloudTrail, S3,
    and Kinesis
