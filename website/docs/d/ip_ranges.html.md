---
layout: "cloudflare"
page_title: "CloudFlare: cloudflare_ip_ranges"
sidebar_current: "docs-cloudflare-datasource-ip_ranges"
description: |-
  Get information on CloudFlare IP ranges.
---

# cloudflare_ip_ranges

Use this data source to get the [IP ranges][1] of CloudFlare edge nodes.

## Example Usage

```hcl
data "cloudflare_ip_ranges" "cloudflare" {}

resource "google_compute_firewall" "allow_cloudflare_ingress" {
  name    = "from_cloudflare"
  network = "default"

  ingress {
    ports         = "443"
    protocol      = "tcp"
    source_ranges = ["${data.cloudflare_ip_ranges.cloudflare.cidr_blocks}"]
  }
}
```

## Attributes Reference

- `cidr_blocks` - The lexically ordered list of all CIDR blocks.

- `ipv4_cidr_blocks` - The lexically ordered list of only the IPv4 CIDR blocks.

- `ipv6_cidr_blocks` - The lexically ordered list of only the IPv6 CIDR blocks.

[1]: https://www.cloudflare.com/ips/
