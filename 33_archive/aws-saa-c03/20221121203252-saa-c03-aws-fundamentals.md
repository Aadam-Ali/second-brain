---
id: 20221121203252
tags: [aws-saa-c03]
---

# AWS Fundamentals (SAA-C03)

## Building Blocks

* Region - a physical location that consists of two or more AZs
* Avalibility Zone - one or more discrete data centres, with redundant
  power, networking, and connectivity
* Edge locations - endpoints used by AWS for [[20230608191203-saa-c03-caching|caching]]
  content, think CloudFront

## Shared Responsibility Model

* If something can be done in the AWS console, it's the customer's
  responsibility
* If not, it's AWS's responsibility
* Encryption is a shared responsibility

## Key Services

* Compute - [[20221204122753-saa-c03-elastic-cloud-compute-ec2|EC2]], Lambda, Elastic
  Beanstalk
* Storage - [[20221203141054-saa-c03-simple-storage-service-s3|S3]],
  [[20221205171813-saa-c03-elastic-block-storage-ebs-elastic-file-system-efs|EBS, EFS, FSx]], Storage Gateway
* Databases - [[20221208210554-saa-c03-databases|RDS, DynamoDB]], Redshift
* Networking - [[20230210110617-saa-c03-virtual-private-cloud-vpc|VPC]], Direct
  Connect, [[20230212133907-saa-c03-route-53|Route 53]], API Gateway, AWS Global
  Accelerator

Related:

  * Well-Architected Framework White Paper
    <https://docs.aws.amazon.com/pdfs/wellarchitected/latest/framework/wellarchitected-framework.pdf#welcome>
