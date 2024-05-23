---
id: 20230210110617
tags: [aws-saa-c03, vpc, networking]
---

# Virtual Private Cloud (VPC)

## VPC Fundamentals

* Logically isolated part of the AWS cloud where you can define your own
  network
* 1:1 mapping of subnet and AZs
* Complete control over network, IP addresses, subnets, route tables,
  and network gateways
* Can assign IP addresses to subnets
* Can configure route tables between subnets
* Can attatch internet gateways (IGW) to achieve internet connectivity
* Can control access using ACLs (can be used to block specific IP
  addresses)

## Default VPC vs Custom VPC

* *Default*
  * User friendly
  * All subnets have internet connectivity
  * EC2 instances have public and private IP addresses
* *Custom*
  * Completely customisable
  * Longer setup


## NAT Gateway

* Used to allow instances in private subnets to connect to the internet
  or other AWS services without allowing inbound connections from the
  internet
* Is placed in a public subnet
* Redundant in the AZ
* 5Gbps - 45Gbps speeds
* Managed by AWS
* No association with security groups
* Automatically assigned a public IP
* If a NAT GW AZ goes down, all resources using the NAT GW will lose
  internet access (avoid by having a NAT GW in each AZ and route
  resources to use the NAT GW in their own AZ)

## Network ACLs

* An optional layer of security for a VPC that acts like a firewall for
  controller inbound and outbound traffic for one or more subnets
* Subnets can only be associated to a single ACL
* Might set up with rules similar to a security group for an extra layer
  of security
* Default ACL allows all inbound and outbound traffic
* Custom ACLs deny all inbound and outbound traffic by default
* Each subnet in a VPC must be associated with an ACL (falls back to
  default if not)
* Can block IP addresses unlike security groups
* Contain a numbered list of rules that are evaluated in ascending order
  (where the lowest number rules take presedence)
* Seperate inbound and outbound rules that can allow/deny traffic
* They are stateless, responses to inbound traffic are dependant on
  rules for outbound traffic and vice versa

## VPC Endpoints

* Enables private connections between a VPC to supported AWS Services
  and VPC endpoint services powered by PrivateLink without IGW, NAT GW,
  VPN, or Direct Connect connection
* Ensures traffic stays within the AWS network
* Endpoints are virtual devices that are horizontally scaled, redundant,
  and highly available VPC components that allow conenctions between a
  VPC and other services without bandwidth constraints or availability
  risks
* Two types of endpoints, interface and
  * Interface endpoints - elastic network interface with a private IP
    address for supported AWS services
  * Gateway endpoints - A virtual device provisioned by a user, supports
    S3 and DynamoDB

## VPC Peering

* Allows the connection of one VPC with another via a direct network
  route using private IP addresses
* Effectively means that instances in either VPC are on the same network
* VPCs can be peered within the same account or cross account or cross
  region
* Peering uses a star configuration (no transitive peering)

## Private Link

* Used when required to peer VPCs to many (10s, 100s, 1000s) customer
  VPCs
* Does not require VPC peering: no route tables, NAT GWs, IGWs, etc.
* Requires a NLB on the service VPC and an ENI on the customer VPC

## VPN CloudHub

* Used if you have multiple sites with individual VPN connections that
  need to be connected
* Uses the hub and spoke model
* Low cost and easy to manage
* Operates over the internet, all traffic between a customer GW and
  CloudHub is encrypted

## Direct Connect

* A dedicated network connection between on premises and AWS
* Can reduce network costs, increase throughput, improve connection
  consitency since there is a direct line between on premises and AWS
* Two types of connection:
  * Dedicated connection - a physical ethernet connection associated
    with a single customer, can be requested through the console, CLI,
    or API
  * Hosted connection - a physical ethernet connection that an AWS
    Direct Connect Partner provisions for a customer, whoc request a
    connection by contactinga partner in the AWS Direct Connect Partner
    Program.
* VPN vs Direct Connect:
  * VPN goes over the internet and can be slow at times
  * Direct connect is fast, secure, reliable, and can take massive
    throughput

## Transit Gateway

* Allows transitive peering between thousands of VPCs and on prem data
  centers
* Uses the hub and spoke model
* Works on a regional basis but can be used cross region
* Can be used cross account using Resource Access Manager
* You can use route tables limit VPC communication
* Works with Direct Connect and VPN connections
* Supports IP multicast (only AWS service to do so)
* Mainly used for audio and video distribution
* Simplifies a network topology

## AWS Wavelength

* Embeds AWS compute and storage services within 5G networks
* Provides mobile edge computing infrastructure for ultra-low-latency applications
