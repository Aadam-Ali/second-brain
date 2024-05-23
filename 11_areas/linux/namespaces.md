---
id: 20240323145547
tags: [linux]
---

# Namespaces

Namespaces are a feature of the Linux kernel that allow processes to see
different sets of resources. They work by making it appear to a process
that it has it's own isolated instance of the global resource.  Changes
to resources in a namespace are only visible to processes running within
the namespace not those running in another namespace.

There are currently 8 namespaces:
* **Cgroup** - Hides the identity of the control group that the process is
a member of
* **IPC (Inter-process communication)** - Isolates certain IPC resources,
specifically, SystemV IPC objects and POSIX message queues
* **Network** - Isolates system resources relating to networking
* **Mount** - Controls mount points
* **PID** - Provides an independent set of process IDs
* **Time** - Allows processes to view different system times
* **User** - Isolates security-related identifiers and attributes thus
providing privilege isolation
* **UTS** - Provides isolation of two system identifiers: hostname and NIS
domain name

Related:
  * [[cgroups]]
