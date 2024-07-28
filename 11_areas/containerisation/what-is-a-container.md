---
id: 20240707090628
tags: [containers]
---

# What is a container?

A container is a standard package of software that contains all
necessary application code (or an application binary), runtimes,
dependencies, and configuration files to run said application.

Containers leverage Linux kernel features such as [[namespaces]] and [[cgroups]]
in order to isolate processes and allocate resource (CPU, memory, disk
etc.). This allows containers to virtualise the operating system
(usually Linux), which allows containers to be more lightweight and
portable when compared to virtual machines.

Related:
