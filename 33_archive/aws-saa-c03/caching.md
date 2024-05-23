---
id: 20230608191203
tags: [aws-saa-c03, caching]
---

# Caching

## Where To Cache?

* External - caching data that is returned to users e.g. static content,
  images, and videos
* Internal - speeding up calls to databases

## CloudFront

* CloudFront defaults to HTTPS, with the ability to use custom SSL
  certificates
* CloudFront is the only way to serve static S3 websites using HTTPS
* CloudFront distributes content in general areas, contitnents not
  countries
* CloudFront can be used to block individual countries
* Supports both AWS and non AWS applications
* Can set an expiry date (TTL) for content, which can be manually
  overidden if necessary
* Can use signed URLS or cookies to add temporary access to content
* Improves response times for customers

## ElastiCache

* ElastiCache can be put in front of most databases but is most
  performant in front of RDS
* ElastiCache is an AWS managed version of Memcached or Redis
* Memcached:
  * Database caching solution
  * Can not function as a standalone database
  * No failover or multi AZ support
  * No backups
* Redis:
  * Supports caching
  * Functions as a standalone database
  * Failover and multi AZ support
  * Supports backups

## DynamoDB Accelerator (DAX)

* As suggested by the name, DAX only supports DynamoDB
* An in-memory cache which can reduce response times from milliseconds
  to microseconds
* DAX is highly available
* DAX lives within a VPC
* Does not support backups
* User determines the node size and count for the cluster, TTL for
  data, and maintenance windows for updates

## Global Accelerator

* Global Accelerator is a networking service that sends user traffic
  through AWS's global network infrastructure, increasing performance
  and helping with IP caching
* Global Accelerator assigns two static IPs which sit in front of
  infrastructure
* Abstracts away from complex infrastructure, which is constantly
  changing
* Users can create weighted groups behind IPs to test new features and
  handle failures
