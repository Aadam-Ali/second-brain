---
id: 20230309161615
tags: [aws-saa-c03, asg]
---

# High Availability and Scaling

## Horizontal vs. Vertical Scaling

* Vertical scaling is increasing the size (e.g. using a bigger EC2
  instance type)
* Horizontal scaling is increasing the amount
* Horizontal scaling is more suitable for HA systems

## The 3 W's of Scaling

* What - What do we scale? (which resource)
* Where - Where do we scale? (which vpc / subnet)
* When - When do we scale? (which alarms)

## Launch Templates and Configuration

* Launch templates specify all the required settings to provision an
  EC2 instance
* Launch Templates:
  * More than autoscaling
  * Supports versioning
  * More granularity
  * More recent
  * Recommended by AWS
* Launch Configurations:
  * Only for autoscaling
  * Immutable
  * Limited configuration options
* Launch templates can include information about the AMI, instance size,
  security groups, networking information, and user data
* Launch configurations do not include networking information just
  security groups

## Autoscaling

* Auto scaling groups are a collection of EC2 instances used to aid
  scaling and administration
* Creating auto scaling groups:
  * Define a template
  * Networking and purchasing (use at least 2 AZs, ASG will balance
    across AZs)
  * ELB configuration (should use ELB health check)
  * Set scaling policies
  * Notifications (using SNS)
* Minimum is the lowest number of instances, should generally be set to
  2 (in different AZs)
* Maximum is highest number of instances, should be careful when
  choosing to avoid unexpected costs
* Desired is the current required number
* Can choose between On Demand and Spot instances
* Autoscaling is key to creating a HA application

## Auto Scaling Policies

* Warm up prevents instances from being placed behind the load balancer
* Cooldown prevents auto scaling to prevent rapid scale out, scale in
* These avoid thrashing, where scaling in then out happens in quick
  succession
* Reactive scaling - scale based on data points (CloudWatch)
* Scheduled scaling - used for predicitve workloads
* Predictive scaling - uses machine learning to determine when to scale
* Steady state scaling - min, max, and desired capacity are equal
* Scale out aggressively, scale in conservatively
* Reduce provisioning times by using purpose built AMIs
* Use Reserved Instances for minimum capacity of instances

## Scaling Relational Databases

* Vertical Scaling - increase the size of the database instance
* Scaling Storage - can be resized, only increased
* Read Replicas - can create read-only copies of data (use multiple AZs)
* Aurora Serverless - hand over scaling to AWS, great for unpredictable
  workloads
* When possible use Aurora

## Scaling Non-Relational Databases

* DynamoDB is an AWS managed service thus scaling is much simpler
* Provisioned Capacity - used for predictable workloads by setting an
  upper and lower bound, most cost effective
* On-Demand Capacity - used for sporadic workloads by enabling on-demand
  scaling, you have to pay per read and write
* Can switch between On-Demand and Provisioned once every 24 hours
* Avoiding hot keys will lead to better performance
* Consider cost when deciding which table to use
