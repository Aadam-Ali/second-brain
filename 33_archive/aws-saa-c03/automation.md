---
id: 20230606190518
tags: [aws-saa-c03, automation]
---

# Automation

## Why Automate? And What Are The Benefits?

* Manually carrying out steps is prone to human error
* You can focus on more important tasks since you don't have to manually
  execute processes
* Reduces the risk of introducing security vulnerabilites
* Allows for consistent reproduction

## CloudFormation

* A declarative programming language, supports JSON and YAML
* Used to provision immutable infrastructure
* Templates consist of parameters, mappings, and resources
* Templates are automatically stored in S3
* Hard coded values can be a point of failure when deploying in multiple
  regions, mappings can be used to avoid this by providing region
  specific values
* If an error occurs during a deployment, CloudFormation will rollback
  to the last known good state

## Elastic Beanstalk

* Simplifies the deployment of applications, only need to provide code
* It automatically deploys applications, configuration can be in the
  form of a template
* Can handle testing applications in a staging environment before
  deploying to production
* Automatically provisions EC2 instances and their underlying OS

## Systems Manager

* A set of tools to view, control, and automate AWS architecture and
  on-prem resources
* Features (include but are not limited to):
  * Automation Documents (Runbooks) - can used to control EC2 instances,
    or other AWS resources
  * Run Command - execute commands on hosts
  * Patch Manager - manages application versions
  * Parameter Store - securely store secret values
  * Hybrid Activations - control on-prem architecture using Systems
    Manager
  * Session Manager - remotely connect to EC2 instances without SSH
