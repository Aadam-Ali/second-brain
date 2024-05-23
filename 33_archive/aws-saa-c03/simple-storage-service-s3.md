---
id: 20221203141054
tags: [aws-saa-c03, s3]
---

# Simple Storage Service (S3)

## Key Points

* Object-based storage allows you to upload files
* Not suitable for running an OS or DB
* Files can be up to 5TB in size
* Unlimited storage

## Buckets

* Files are stored in buckets (with globally unique names)
* Successful uploads via the CLI or API will return a 200 HTTP status
  code

## Object Tips

* Key - An object's name (e.g. hello-world.txt)
* Value - The data itself, composed of a sequence of bytes
* Version ID - Allows the storage of multiple versions of an object
* Metadata - Data about the type of data (e.g. content-type or
  last-modified)

## Securing an S3 Bucket

* By default buckets are private (as well as the objects within), public
  access has to be granted to both buckets and objects to make the
  bucket public
* Individual objects can control access using Object ACLs (e.g. can
  make an object public)
* Entire buckets can be made public using bucket policies

## Hosting a Static Webiste

* Make bucket public using a bucket policy
* You can only serve static content
* Automatic scaling based on demand

## Versioning Objects

* All versions are stored in S3 (even for deleted object)
* Is useful for the back up of data
* Once enabled, versioning can only be suspended (not disabled)
* Versioning can be integrated with lifecycle rules
* Supports MFA

## Storage Tiers

| Storage Class                 | Availability and Durability            | AZ(s) | Use Case                                                                                                       |
|-------------------------------|----------------------------------------|-------|----------------------------------------------------------------------------------------------------------------|
| S3 Standard                   | 99.99% Availability - 11 9s Durability | >=3   | Suitable for most workloads (e.g. websites, content distribution etc.)                                         |
| S3 Standard-Infrequent Access | 99.9% Availability - 11 9s Durability  | >=3   | Long term, infrequently accessed critical data (e.g. backups, disaster recovery)                               |
| S3 One Zone-Infrequent Access | 99.5% Availability - 11 9s Durability  | 1     | Long term, infrequently accessed, non critical data                                                            |
| S3 Glacier                    | 99.99% Availability - 11 9s Durability | >=3   | Long term data archiving that occasionally needs to be accessed in a few hours or minutes                      |
| S3 Glacier Deep Archive       | 99.99% Availability - 11 9s Durability | >=3   | Rarely accessed data archiving with default retrieval time of 12 hours (e.g. records for regulatory purporses) |
| S3 Intelligent-Tiering        | 99.9% Availability - 11 9s Durability  | >=3   | Unknown or unpredictable access patterns                                                                       |

## Lifecycle Management

* Automates the moving of objects between storage tiers (Only from more
  frequent to less frequent)
* Can be used in conjunction with versioning
* Can be applied to current and previous versions of objects

## S3 Object Lock and Glacier Vault Lock

* Use object lock to store objects using a write once, read many (WORM)
  model
* Object lock can be on individual objects or applied across a bucket
* Object lock had two modes: governance and compliance
  * Governance Mode - Users can't overwrite or delete an object version
    or alter it's lock settings unless they have special permissions
  * Compliance Mode - A protected object version can't be overwritten or
    deleted by any user, including the root user
* Glacier Vault Lock allows customers to deploy compliance controls for
  individual S3 Glacier Vaults with a vault lock policy, can specify
  controls like WORM and lock the policy from future edits.

## Encryption

* Encryption in Transit via SSL/TLS
* Encryption at Rest - SSE via SSE-S3 (AES 256-bit), SSE-KMS, or SSE-C
* Client-Side encryption - customer encrypts files before uploading them
* Encryption can be enforced with a bucket policy by rejecting `PUT`
  reqeusts that don't include the `x-amz-server-side-encryption` header

## Optimising S3 Perfomance

* Use multiple prefixes - 3500 PUT/COPY/POST/DELETE and 5000 GET/HEAD
  requests per second, per prefix (e.g. buck/f1/sf1/ or buck/f2/sf1/)
* If using SSE-KMS, customers must take KMS limits into account
  * Uploading/downloading objects will count towards the KMS quota
  * Quota is region specific, usually 5500, 10,000, or 30,000 per second
  * Cannot request to increase the quota
* Use multipart uploads to upload parts in parallel (optional from 100MB
  and required from 5GB)
* Use byte-range fetches to download parts in parallel

## S3 Replication (Formerly Cross-Region Replication)

* You can replicate objects from one bucket to another
* Objects in an existing bucket are not replicated automatically
* Delete markers are not replicated by default
