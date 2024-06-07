---
id: 20221205171813
tags: [aws-saa-c03, ebs, efs]
---

# Elastic Block Storage (EBS) / Elastic File System (EFS) (SAA-C03)

## EBS Volume Types

* gp2 (General Purpose SSD)
  * Suitable for boot disks and general applications
  * Up to 16,000 IOPS per volume
  * Up to 99.99% durability
* gp3 (General Purpose SSD)
  * Suitable for high performance applications
  * Predictable 3000 IOPS baseline and 125MiB/s for all volume sizes
  * Up to 99.99% durability
* io1 (Provisioned IOPS SSD)
  * Suitable for online transaction processing and latency-sensitive
    applications
  * 50 IOPS/GiB
  * Up to 64,000 IOPS per volume
  * High performance and cost
* io2 (Provisioned IOPS SSD)
  * Suitable for same use cases as io1
  * 500 IPS/GiB
  * Up to 64,000 IOPS per volume
  * 99.999% Durability
* st1 (Throughput Optimised HDD)
  * Suitable for big data, data warehouses etc.
  * Max throughput is 500MB/s per volume
  * Cannot be a boot volume
  * Up to 99.9% durability
* sc1 (Cold HDD)
  * Max throughput of 250MB/s per volume
  * Less frequently accessed data
  * Cannot be a boot volume
  * Lowest cost
  * Up to 99.9% durability

## EBS Volumes and Snapshots

* Volumes exist on EBS, whereas snapshots exist on
  [[20221203141054-saa-c03-simple-storage-service-s3|S3]]
* Snapshots only contain changes from the previous snapshot
* Best practice is to stop an instance and detach the volume before
  taking a snapshot
* Snapshots can be shared across accounts and regions (by copying them)
* Volume size and type can be changed on the fly

## EBS Encryption

* Data at rest is encrypted inside the volume
* All in flight data between an instance and a volume is encrypted
* All snapshots are encrypted
* All volumes created from a snapshot are encrypted (encrypted volumes
  only)
* Encryption Process:
  * Create a snapshot of unencrypted volume
  * Create a copy of snapshot with encrypt option ticked
  * Create AMI from the snapshot

## [[20221204122753-saa-c03-elastic-cloud-compute-ec2|EC2]] Hibernation

* Preserves instance's RAM on persistent storage (EBS)
* Speeds up boot times as OS does not have to be reloaded
* Instance RAM must be less that 150GB
* Includes C, M, and R instance families
* Available for Windows, Amazon Linux 2, and Ubuntu
* Hibernation cannot last more than 60 days
* Available for On-Demand and Reserved instances

## EFS

* Support Network File System version 4 protocol (NFSv4)
* Only pay for the storage that you use (no pre provisioning required)
* Can scale up to petabytes
* Can support thousands of concurrent EFS connections
* Data can be stored across multiple AZs within a region
* Read after write consistency
* Use case - highly scalable shared storage using NFS

## When to use EFS, FSx, and FSx for Lustre

* EFS - when you need distributed, highly resilient for Linux instances
  or Linux based applications
* FSx for Windows - when you need centralized storage for Windows based
  applications such as Sharepoint and other native Microsoft applications
* FSx for Lustre - when you need high performance (speed), high capacity
  distributed storage e.g. HPC, machine learning etc. Can store data
  directly on S3.

## AMIs - EBS vs Instance Store

* Instance store volumes are ephemeral
* Instance store volumes cannot be stopped, if the host fails all data
  is lost
* EC2 instances using EBS volumes can be stopped without losing data
* You can reboot both EBS and Instance Store backed instances
* By default both volume types are deleted on termination of an EC2
  instance, EBS provides an option to keep the root device volume

## AWS Backup

* Consolidation - AWS backup provides a central way to backup AWS
  services such as EC2, EBS, EFS, FSx and AWS Storage Gateway
* Organisations - can use AWS Organisations with AWS Backup to backup
  AWS services across multiple accounts
* Benefits - Centralised controls that allow automation and lifecycle
  policies for data. Better compliance as backup policies can be
  enforced, ensure backups are encrypted and can be audited.
