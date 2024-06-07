---
id: 20240701090822
tags: [python, aws]
---

# Paginating in Boto3

While the boto3 library does provide paginators, they are not available
for every function. Most functions will return either a `NextToken` or
`NextMarker`

The following example is for listing Route53 hosted zones, but can be
adapted for other services and functions.

```python
route53 = boto3.client("route53")
hosted_zones = []
resp = route53.list_hosted_zones()

while resp:
    hosted_zones.extend([zone["Id"] for zone in resp["HostedZones"]])

    resp = (
        route53.list_hosted_zones(Marker=resp["NextMarker"])
        if "NextMarker" in resp
        else None
    )

return hosted_zones[]
```

Related:
