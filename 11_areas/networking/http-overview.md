---
id: 20240130211412
tags: [networking, http]
---

# HTTP Overview

HTTP (Hypertext Transfer Protocol) is an application layer (7) protocol
used to transfer hypermedia data between clients and servers.

HTTP requests consist of:
  * HTTP version
  * URL
  * HTTP method - indicator of the action expected from the server e.g.
    `GET` or `POST`
  * Headers - key-value pairs that contain additional information about
    the request e.g. browser via `user-agent`
  * Body (*optional*) - information being submitted to the server e.g.
    username and password

HTTP responses consist of:
  * Status code - an indicator about the status of the request e.g.
    `200` for `OK` or `404` for `Not Found`
  * Headers - key-value pairs that contain additional information about
    the reponse e.g. `status`
  * Body (*optional*) - information being returned by the server e.g.
    HTML

HTTP conventially uses port 80.

Related:
  * [[osi-model-application-layer-7]]
