---
id: 20240130214111
tags: [networking, https, tls]
---

# HTTPS Overview

HTTPS (Hypertext Transfer Protocol Secure) is the encrypted version of
HTTP. It makes use of TLS to encrypt communication between the client
and server, thus making the transfer of sensitive data safer e.g. online
banking

HTTPS uses TLS (Transport Layer Security) formerly SSL (Secure Socket
Layer) to encrypt communication using public key cryptography, which
leverages two distinct keys to encrypt communication:
  * Public key - accessible by anyone who wants to make a request to a
    server, any data encrypted with this key can **only** by decrypted
    by the private key
  * Private key - this key is owned by the server owner and is kept
    private, it is used to decrypt the data encrypted by the public key

Without HTTPS, communication can be intercepted, and data either stolen
or modified by a malicious actor.

HTTPS conventially uses port 443.

Related:
  * [[http-overview]]
