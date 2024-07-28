---
id: 20221121203252
tags: [aws-saa-c03]
---

# AWS Fundamentals (SAA-C03)

## Building Blocks

* Region - a physical location that consists of two or more AZs
* Avalibility Zone - one or more discrete data centres, with redundant
  power, networking, and connectivity
* Edge locations - endpoints used by AWS for [[saa-c03-caching|caching]]
  content, think CloudFront

## Shared Responsibility Model

* If something can be done in the AWS console, it's the customer's
  responsibility
* If not, it's AWS's responsibility
* Encryption is a shared responsibility

## Key Services

* Compute - [[saa-c03-elastic-cloud-compute-ec2|EC2]], Lambda, Elastic
  Beanstalk
* Storage - [[saa-c03-simple-storage-service-s3|S3]],
  [[saa-c03-elastic-block-storage-ebs-elastic-file-system-efs|EBS, EFS, FSx]], Storage Gateway
* Databases - [[saa-c03-databases.md|RDS, DynamoDB]], Redshift
* Networking - [[saa-c03-virtual-private-cloud-vpc|VPC]], Direct
  Connect, [[saa-c03-route-53|Route 53]], API Gateway, AWS Global
  Accelerator

Related:

  * Well-Architected Framework White Paper
    <https://docs.aws.amazon.com/pdfs/wellarchitected/latest/framework/wellarchitected-framework.pdf#welcome>
