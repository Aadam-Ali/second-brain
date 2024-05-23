---
id: 20230305150147
tags: [aws-saa-c03, elb]
---

# Elastic Load Balancing (ELB)

## Overview

* ELB distributes incoming traffic across a set of targets, can be done
  across AZs
* Application Load Balancer - best for HTTP(S), operates at layer 7
  (application), and are application aware; ALB is an intelligent LB
* Network Load Balancer - Operates at layer 4 (transport), capable of
  handling millions of requests per second with ultra low latencies;
  NLB is a performance LB
* Classic Load Balancer - Legacy LB, can load balance HTTP(S) apps while
  using L7 specific features (X-Forwarded and sticky sessions); CLB is a
  classic/dev/test LB
* All LBs can be configured with health checks (periodic requests to
  targets), healthy targets have the `InService` status and unhealthy
  targets have the `OutOfService` status
* Traffic is only routed to `InService` targets

## Application Load Balancers (ALB)

* L7 load balancing - LB receives request, evaluates the listener rules
  to determine which to apply, and then selects a target from the target
  group to route traffic to
* Listeners check for connection requests from clients, using the set
  protocol and port
* Users must define a default rule per listener and can define
  additional rules if needed; rules consist of a priority, one or more
  actions, and one or more conditions
* Target groups route requests to one or more registered targets
* ALBs are limited to only HTTP(S)
* To use HTTPS at least one SSL/TLS cert is required on the LB,
  decryption happens at the LB level not the target level
* Does not have static IP by default

## Network Load Balancers (NLB)

* L4 load balancing - LB receives request, selects a target from the
  target group for the default rule, and then attempts to open a TCP
  connection to the target using the port in the listener
  configuration
* Listener checks for connection requests, using the configured port and
  protocol and forwards the request to the target group
* Target groups route requests to one or more registered targets
* Supports TCP, TLS, UDP, TCP_UDP on ports 1-65535
* TLS listeners offload encryption / decryption from the application to
  the LB; if the listener's protocol is TLS exactly one SSL cert must be
  deployed on the listener
* NLBs are best suited for load balancing TCP traffic where extreme
  performance is needed, can handle millions of requests with ultra low
  latencies, or when using non HTTP(S) protocols

## Classic Load Balancer (CLB)

* To see the original IP address of the client the `X-Forwarded-For`
  header is used
* If application stops responding the CLB returns a 504 error, usually
  indicating an issue with the application / database

## Sticky Sessions

* Applied to CLBs
* Allows you to bind a user's session to a specific instance, useful
  when session data is stored on the instance
* Can be applied to ALBs, however, the stickiness is applied to the
  target group rather than a specific target

## Deregistration Delay

* Allows LBs to complete in-flight requests made to de-registering or
  unhealthy instances
* Can be disabled if you want connections to be closed immediately
