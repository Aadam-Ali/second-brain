---
id: 20221121203252
tags: [aws-saa-c03]
---

# AWS Fundamentals

## Building Blocks

* Region - a physical location that consists of two or more AZs
* Avalibility Zone - one or more discrete data centres, with redundant power,
  networking, and connectivity
* Edge locations - endpoints used by AWS for caching content, think
  CloudFront

## Shared Responsibility Model

* If something can be done in the AWS console, it's the customer's
  responsibility
* If not, it's AWS's responsibility
* Encryption is a shared responsibility

## Key Services

* Compute - EC2, Lambda, Elastic Beanstalk
* Storage - S3, EBS, EFS, FSx, Storage Gateway
* Databases - RDS, DynamoDB, Redshift
* Networking - VPC, Direct Connect, Route 53, API Gateway, AWS Global
  Accelerator

Related:

  * Well-Architected Framework White Paper <https://docs.aws.amazon.com/pdfs/wellarchitected/latest/framework/wellarchitected-framework.pdf#welcome>
