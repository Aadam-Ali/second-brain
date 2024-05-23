---
id: 20230503183930
tags: [aws-saa-c03, sqs, sns]
---

# Decoupling Workflows

## Overview

* Tight coupling - where one instance depends on another instance, which
  introduces single points of failure
* Loose coupling - where one instance communicates via other means such
  that it does not depend on one instance e.g. load balancers or message
  queues between layers
* Simple Queue Service (SQS) - fully managed message queuing service
  that enables the decoupling and scaling of applications
* Simple Notification Service (SNS) - fully managed messaging service
  for application-to-application and application-to-person communication
* API Gateway - fully managed service that simplifies API creation,
  publishing, maintenance, monitoring, and security at scale
* Never opt for a tightly coupled solution as it provides no real
  benefits over loosely coupled solutions
* Every layer should be loosely coupled

## Simple Queue Service (SQS)

* SQS is a messaging queue that allows the asynchronous processing of
  requests
* SQS settings:
    * Delivery delay - defaults to 0; can be set up to 15 minutes
    * Message size - 256KB of text in any format
    * Encryption - messages are encrypted in transit by default but not
      at rest
    * Message retention - defaults to 4 days; can be between 1 minute
      and 14 days
    * Long vs. short - long polling isn't the default but is preferred
    * Queue depth - this can be a trigger for autoscaling
    * Visibility timeout - time that item remains in queue without
      consumers being aware of it

## Dead-Letter Queues (DLQ)

* A secondary queue that can be used to sideline messages which reach
  the maximum receives
* The dead letter queue must be created before the main queue
* You should set up a CloudWatch alarm to monitor the queue depth to
  gain visibility when things are going wrong
* Can be used with SNS

## SQS First In First Out (FIFO)

* SQS by default provides best effort ordering which does not guarantee
  messages being consumed in the same order as they were received, also
  there is a risk of messages being duplicated
* With SQS FIFO messages are consumed in the order that they are
  received
* SQS Standard:
    * Best effort ordering
    * Duplicate messages
    * Nearly unlimited transactions per second
* SQS FIFO:
    * Guaranteed ordering
    * No message duplication
    * 300 messages per second
    * Not as performant as standard
    * Higher cost due to compute required to deduplicate messages
* FIFO is the only option when required to enforce message ordering
* Messages can be ordered with a standard queue however it's on the user
  to configure it
* Message Group ID ensures messages are processed one by one

## Simple Notification Service (SNS)

* A pushed-based messaging service which delivers messages to subscribed
  endpoints
* SNS settings:
    * Subscribers - Kinesis Data Firehose, SQS, Lambda, email,
      HTTP(S), SMS, or a platform application endpoint
    * Message size - 256KB of text in any format
    * DLQ support - Messages that fail to be delivered can be placed
      onto an SQS DLQ
    * FIFO - FIFO SNS topics only support SQS as a subscriber
    * Encryption - messages are encrypted in transit by default but not
      as rest
    * Access policy - a resource policy which controls who or what can
      publish to an SNS topic
* SNS can be used to send alerts
* SNS can be used with CloudWatch to send alerts when alarms go off
* SNS will only retry HTTP(S) endpoints, for other subscribers messages
  should be sent to an SQS DLQ if they are required

## API Gateway

* API Gateway is fully managed service that simplifies API creation,
  publishing, maintenance, monitoring, and security
* Allows protection of endpoints by attaching a web application firewall
  (WAF)
* Can implement rate limiting and DDoS protection to reduce abuse of
  endpoints
* Is simple to start building with
* Supports versioning of APIs
* Removes the need to bake credentials into code

## AWS Batch

* An AWS service which allows you to run batch computing workloads with
  EC2 or ECS/Fargate
* Abstracts the configuration and management of infrastructure away from
  the user
* Automatically provisions, scales and distributes workloads based on
  number of submitted jobs
* No installation is required
* Components:
    * Jobs - units of work e.g. shell scripts, executables, and Docker
      images
    * Job definitions - specify how job are to be run
    * Job queues - where jobs are submitted to reside until they are run
    * Compute environment - compute resources used to run jobs
* Fargate is the recommended way of launching _most_ batch jobs,
  although EC2 is sometimes the better choice
* When EC2 is better:
    * When a custom AMI is required
    * When >4 vCPUs are required
    * When >30GB of memory is required
    * When a GPU or Graviton CPU is required
    * When using `linuxParameters` parameters
    * For a large number of jobs as it will have better concurrency
      limits
* AWS Batch vs Lambda:
    * Lambda has a 15 minutes execution limit, Batch does not
    * Lambda has limited disk space, and EFS requires a Lambda to be in
      a VPC
    * Lambda is fully serverless but it has limited runtimes by default
    * Batch used Docker, so any runtime can be used
* Managed compute environment:
    * AWS manages capacity and instance types
    * Resource specifications are defined when an environment is created
    * ECS instances are launched into VPC subnets
    * Default is the most recent, approved Amazon ECS AMI
    * You can use your own AMI (must meet specifications)
    * Can use Fargate, Fargate Spot, or standard Spot instances
* Unmanaged compute environment:
    * User manages resources
    * AMI must meet Amazon ECS AMI specs
    * Less commonly used
    * Is used for extremely complex or specific requirements

## Amazon MQ

* Managed message broker service which aids migration of existing
  applications
* Uses multiple programming languages, OSes, and messaging protocols
  (JMS, AMQP 0-9-1, AMQP 1.0, MQTT, OpenWire, and STOMP)
* Supports Apache ActiveMQ or RabbitMQ engines
* Allows easier migration of exisiting applications as there is no need
  to maintain the service
* SNS with SQS vs Amazon MQ:
    * Both offer topics and queues
    * Both allow one-to-one or one-to-many messaging
    * When migrating applications with messaging systems in place,
      Amazon MQ is the better choice
    * For new applications SNS with SQS is the better choice due to its
      simplicity and scalability
    * Amazon MQ *requires* private networking whereas SNS and SQS are
      public by default
    * Amazon MQ has *no* default AWS integrations
* Single-instance broker - one broker in one AZ, ideal for development
  environments; RabbitMQ has an NLB in front of it
* Highly available - HA architecture to minimise downtime, architecture
  depends on engine
* Amazon MQ for ActiveMQ - active/standby deployments where one instance
  remains available at all time; configure a network of brokers with
  seperate maintenance windows
* Amazon MQ for RabbitMQ - groupings of three broker nodes across
  multiple AZs behing an NLB

## Step Functions

* Step functions is a serverless orchestration service for event-driven
  task executions
* Has a graphical console for easier visualisation
* It has two main components:
    * State machine - a particular workflow with different event-driven
      steps
    * Task - Specific states within a workflow representing a single
      unit of work
* Every step within a worklow is considered a state
* There are two types of workflow
* Standard workflow:
    * Have an exactly-once execution
    * Can run for up to one year
    * Useful for long-running workflows that require an auditable
      history
    * Rates up to 2000 executions per second
    * Pricing based per state transition
* Express workflow:
    * At-least-once execution
    * Can run for up to 5 minutes
    * Useful for high event rate workflows e.g. IoT data streaming
    * Pricing is based on number of executions, durations, and memory
      consumption
* States:
    * States can be used to make decisions based on input
    * States (and workflows) are defined in Amazon States Language (ASL)
    * States are elements within state machines
* Integrates with multiple services such as Lambda, Batch, DynamoDB and
  so on
* Types of state:
    * Pass - passes any input to its output, no work done
    * Task - single unit of work performed (e.g. Lambda, Batch, and SNS)
    * Choice - adds branching logic to state machines
    * Wait - creates a specified time delay within the state machine
    * Succeed - stops executions successfully
    * Fail - stops executions and marks them as failures
    * Parallel - Runs parallel branches of executions within state
      machines
    * Map - runs a set of steps based on elements of an input array

## Amazon AppFlow

* A fully managed service for exchanging data between SaaS apps and AWS
  services
* Pulls data records from SaaS vendors and stores them in S3
* Bi-directional data transfer with limited source / destination
  combinations
* Flows transfer data between sources and destinations
* Data mappings determine how source data is stored
* Filters are criteria that control which data is transferred
* Triggers are what start the flow
* Use cases of AppFlow:
    * Transferring Salesforce records to Amazon Redshift
    * Ingesting and analysing Slack conversations in S3
    * Migrating Zendesk and other help desk support tickets to Snowflake
    * Transferring aggregate data on scheduled basis to S3 (up to 100GB
      per flow)
