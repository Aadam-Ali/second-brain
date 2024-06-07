---
id: 20230520143731
tags: [aws-saa-c03, serverless]
---

# Serverless Architecture (SAA-C03)

## Serverless Overview

* Allows the offloading of the operating system to AWS
* Benefits:
  * Ease of use - most things are handled by AWS
  * Event based - resources are only spun up ad-hoc
  * Billing model - you only pay for what you actually use

## Lambda

* A serverless compute services that allows you to run code without
  managing or provisioning servers
* Building a function:
  * Runtime - the environment in which code runs in, can be AWS provided
    or build your own
  * Permissions - a role will need to be attached if the Lambda
    interacts with AWS APIs
  * Networking - can optionally define configuration if it needs access
    to private resources
  * Resources - selecting an amount of memory (10GB max) will determine
    the amount of CPU and RAM available to the function
  * Trigger - the event / resource that will cause an execution of the
    code

## AWS Serverless Application Respository

* A service to allow users to easily find, deploy, and publish
  serverless applications
* Can privately and publicly share applications
* Upload both application code and a manifest file called a SAM template
* Integrated with Lambda
* Publish:
  * Making apps available for people to find and deploy
  * Define apps using SAM templates
  * Private by default
  * Must explicitly share if needed
* Deploy:
  * Find and deploy published applications
  * Public apps can be browsed without an AWS account
  * Browse in the AWS Lambda console
  * Don't automatically trust applications

## Container Overview

* A container is small piece of software which contains packaged up code
  and its dependencies to make running it in different environments more
  reliable
* Dockerfile - a set of instructions that determines the contents of an
  image
* Image - an immutable file which contains the code, dependencies, and
  configuration required to run the code
* Registry - a service which stores Docker images
* [[20240707090628-container|Container]] - a running instance of an image


## Elastic Container Service (ECS)

* Can manage thousands of containers
* Containers are (de)registered with
  [[20230305150147-saa-c03-elastic-load-balancing-elb|ELBs]] when they come online / go
  offline
* Containers can have roles attached to them if they need to speak to
  other AWS services
* Easy to set up and scale appropriately to workload

## Elastic Kubernetes (K8s) Service (EKS)

* Kubernetes is an open source alternative to ECS, meaning it can also
  be run on prem
* EKS is a managed version of Kubernetes
* Requires more work to configure and integrate than ECS

## Fargate

* A serverless compute engine for containers that works with both ECS
  and EKS
* [[20221204122753-saa-c03-elastic-cloud-compute-ec2|EC2]]:
  * Benefit from the EC2 pricing model - RIs, savings plans etc.
  * Better for long running workloads
  * Multiple containers can be run on the same host
  * You have to manage the OS yourself
* Fargate:
  * No OS access
  * Pay based on allocated resource and runtime
  * Better for short running tasks
  * Isolated environments
* Fargate vs Lambda:
  * Fargate should be selected for more consistent workloads
  * Fargate offers greater control for developers since they can run
    Docker locally
  * Lambda is better for inconsistent workloads
  * Lambda is better for smaller apps that can expressed as a single
    function

## EventBridge (formerly CloudWatch Events)

* A serverless event bus which allows you to pass events from a source
  to an endpoint
* Creating a rule:
  * Select how you want the rule to be invoked e.g.
    an event or schedule
  * Select what type of event it will be AWS service event, a custom
    event, or a partner event (e.g. from a SaaS application)
  * Select the target of the event
  * Tag the the rule
* Commonly used to trigger Lambda functions when AWS API calls happen
* Quickest method to act on events happening in an environment

## Elastic Container Registry (ECR)

* A managed container image registry that offers secure, scalable, and
  reliable infrastructure
* Stores private container image repositories with IAM resource-based
  permissions
* Supports OCI images, Docker images, and OCI artifacts
* Components:
  * Registry - a private registry is provided to every account, can
    create more
  * Authorisation token - a token required for pushing and pulling
    images from registries
  * Repository - this is what contains the images
  * Repository policy - controls access to repositories and images
* Amazon ECR Public is a similar service for public image repositories
* Features:
  * Lifecycle policies - helps management of images in repositories by
    defining rules (which can be tested) for cleaning up unused images
  * Image scanning - helps identify CVEs on push (if set) by generating
    reports which can be accessed later on
  * Sharing - supports cross-region and cross-account support, this is
    configured per repository per region
  * Cache rules - can pull through cache rules to allow caching public
    images privately on a regular cadence
  * Tag mutability - prevents images tags from being overwritten,
    configured per repository
* Integrates with existing container infrastructure, ECS, EKS, and
  Amazon Linux containers

## Amazon EKS Distro

* A Kubernetes distribution based on and used by EKS (same versions and
  dependencies)
* Fully managed by the customer and can be run anywhere e.g. cloud or
  on-prem
* It is the customers responsiblity to upgrade and manage versions

## Amazon EKS Anywhere

* On-prem way to manages K8s clusters
* Based on EKS distro
* Offers full lifecycle management of multiple K8s clusters
* Operates independently of AWS
* K8s control plane is managed by the customer in their own data centre
* Updates are done via the manual CLI or Flux
* Curated packages offer extended core functionalities of K8s clusters,
  but require an enterprise subscription

## Amazon ECS Anywhere

* Allows the management of containerised apps on-prem
* Removes the requirement to install and manage container orchestration
  software
* Completely managed solution enabling the standardisation of container
  management across environments
* No ELB support thus the customer has to manage inbound traffic routing
* Introduces the `EXTERNAL` launch type for creating services and
  running tasks
* Requirements:
  * Must have SSM Agent, ECS agent, and Docker installed
  * Must register external instances as SSM Managed Instances
  * Can create an installation script with the ECS console to make the
    process simpler
  * Scripts contain SSM activation keys and commands to install required
    software
  * Execute scripts on on-prem VMs or bare metal servers
  * Deploy containers using the `EXTERNAL` launch type

## Amazon Aurora Serverless

* On-demand, auto-scaling configuration for Aurora
* Charged per-second based on resource utilisation thus making it budget
  friendly
* Aurora Capacity Units (ACUs) - measurements on how your clusters
  scale, set a maximum and minimum (can be zero)
* ACUs consist of ~2GB of memory, matching CPU, and networking
  capabilities
* ACUs are allocated quickly by AWS-managed warm pools
* As resilient as Aurora provisioned - six copies of data across three
  AZs
* Use cases - variable workloads, multi-tenant apps, new apps, test
  environments, and capacity planning

## AWS X-Ray

* Collects application data to gain insights about requests and
  responses
* View downstream calls to AWS resources, other services/APIs, or DBs
* Receives traces from applications for allowing insights
* Integrated services can add tracing headers, send trace data or run
  the X-Ray daemon
* Concepts:
  * Segments - data containing resource names, request details, and
    other information
  * Subsegments - Segments providing more granular timing information
    and details
  * Service graph - Graphical view of interacting services
  * Traces - trace ID tracks paths of requests and traces collect all
    segments in a request
  * Tracing header - Extra HTTP header `X-Amzn-Trace-Id` containing
    sampling desicions and trace ID
* The X-Ray daemon listens on UDP port 200, collecting raw segment data
  which it sends to the X-Ray API
* The X-Ray daemon can be installed on EC2 and ECS tasks, toggled for
  Lambda, configured with Elastic Beanstalk, added to stages on API
  Gateway, and integrated with SQS and SNS to view time taken for
  messages

## AWS AppSync

* A robust, scalable GraphQL interface for application developers
* Combines data from multiple sources e.g. Lambda and DynamoDB
* Enables developers to interact with their data via GraphQL
* GraphQL - a data language that enables apps to fetch data from servers
* Integrates seamlessly with React, React Native, iOS, and Android
