---
id: 20221204122753
tags: [aws-saa-c03, ec2]
---

# Elastic Cloud Compute (EC2)

## What is EC2?

* EC2 allows you to have VMs hosted in AWS
  * Can select the capacity required in the current moment
  * Grow and shrink capacity as necessary
  * Only pay for what you use
  * Takes minutes to provision as opposed to days/weeks/months (on prem)

## Pricing Options

| Type      | Price / Payment                                                         | Use Case                                                      |
|-----------|-------------------------------------------------------------------------|---------------------------------------------------------------|
| On-Demand | Pay by the hour, depends on instance type                               | Flexible workloads, testing / spiky workloads                 |
| Spot      | Unused capacity at a discount of up to 90% (based on supply and demand) | Flexible start and end times, cost sensitive, urgent capacity |
| Reserved  | Up to 72% discount on hourly charge                                     | Known, fixed requirements                                     |
| Dedicated | On-Demand or Reserved (up to 70% discount)                              | Server bound licensing or compliance requirements             |

## IAM Roles

* Preferred option to provide EC2 access to other AWS services from a
  security POV
* Avoids hard coding credentials in the instance
* Policies control a role's permissions and can be updated with
  immediate effect
* Can attach and detach roles without having to stop/terminate instances

## Security Groups

* Changes to security groups are effective immediately
* You can have any amount of EC2 instances in a security group
* You can have multiple security groups on an EC2 instance
* By default, all inbound traffic is blocked and all outbound traffic is
  allowed

## User Data (Bootstrap Script) & Metadata

* User data is a script which runs when the instance first runs, commonly
  used to update the OS and install required packages
* Metadata is data about your EC2 instances such as IP address and hostname
* Metadata can be accessed via user data (via `curl
  http://169.254.169.254/latest/meta-data/<attribute>`)

## Networking

* ENI (Elastic Network Interface) - For basic networking, allows
  seperation of networks at a low cost by using multiple ENIs in each
  network
* Enhanced Networking - For speeds between 10Gbps - 100Gbps, for
  reliable, high throughput
    * ENA (Elastic Network Adapter) supports speeds up to 100Gbps
    * Intel VF (virtual function) Interface supports speeds up to 10Gbps
      and is typically used on older hardware
* EFA (Elastic Fabric Adapter) - When you need to accelerate High
  Performance Computing (HPC) or ML applications, or you need to do an
  OS-Bypass.

## Placement Groups

* Cluster - Low network latency and/or high network throughput
  * Can't span across AZs unlike spread and partition
  * AWS recommends using cluster with homogenous instances
* Spread - Individual critical EC2 instances
* Partition - Multiple EC2 instances; HDFS, HBase, and Cassandra
* Only certain instance types can be launched in a placement group
  (compute, memory, and storage optimised, and GPU)
* You cannot merge Placement Groups
* You can move stopped instances into a Placement Group via the CLI or
  SDK (but not the console as of now)

## Spot Instances

* Useful for any type of computing where persistence isn't required
* You can block spot instances from terminating using a Spot Block (for
  1-6 hours after spot price exceeds the maximum)
* A Spot Fleet is a collection of Spot Instances and (optionally)
  On-Demand instances

## VCentre

* You can deploy vCenter on the AWS Cloud using VMWare to either migrate
  or manage hybrid workloads

## AWS Outposts

* Provides the capability to extend AWS to on premises hardware
* AWS Outposts rack for large deployments, think data centres
* AWS Outposts server for smaller deployments, think factories
