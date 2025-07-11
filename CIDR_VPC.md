# VPC CIDR Blocks

## CIDR (Classless Inter-Domain Routing)
- Defines IP address ranges for your VPC.
- Every VPC must have an IPv4 CIDR block.
- You can also associate:
  - Additional IPv4 CIDR blocks
  - IPv6 CIDR blocks (optional)

---

## IPv4 CIDR Blocks

### Creating a VPC
- Must specify an IPv4 CIDR block between `/16` (65,536 IPs) and `/28` (16 IPs).
- Recommended private IPv4 ranges (RFC1918):
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16
- Avoid 172.17.0.0/16 (used by AWS services).

### Adding Secondary IPv4 CIDRs
- Must not overlap with:
  - Existing VPC CIDRs
  - Conflicting routes in route tables
- Block size limits: `/28` to `/16`
- Existing CIDR blocks cannot be resized.

### Route Table Implications
- A local route is automatically added for each CIDR.
- Existing route destinations can restrict new CIDRs.
  - Example: if a route covers 10.0.0.0/24, you can’t add 10.0.0.0/16.

### Quota Limits
- Limits on:
  - Number of CIDR blocks per VPC.
  - Number of routes in route tables.

### Special Scenarios
- VPC Peering:
  - No overlapping CIDRs between peered VPCs.
  - Pending-acceptance peering restricts adding CIDRs.
- Direct Connect Gateways:
  - VPCs must have non-overlapping CIDRs.

### CIDR States
- associating → associated
- disassociating → disassociated
- failing | failed
- Cannot remove the primary CIDR block.

---

## IPv4 CIDR Block Restrictions

| Range | Restrictions |
|-------|--------------|
| RFC1918 Private Ranges | Careful combining different ranges. For example, 10.0.0.0/15 blocks later adding 10.0.0.0/16. |
| 169.254.0.0/16 | Not allowed (link-local). |
| Publicly Routable Blocks | Supported but must avoid conflicts. |

---

## IPv6 CIDR Blocks

- Associate:
  - One IPv6 CIDR when creating the VPC.
  - Up to 5 IPv6 CIDRs (`/44` to `/60`).
- Assigned automatically from Amazon’s IPv6 pool.
  - Example: VPC gets 2001:db8:1234:1a00::/56.
  - Subnets can use `/64` ranges.
- Disassociating IPv6 CIDR:
  - You will likely get a different range if re-added.

---

## Best Practices
- Plan CIDRs to avoid overlaps with:
  - Other VPCs (peering, Direct Connect)
  - AWS internal services
- Prefer private ranges unless needed.
- Document all CIDR assignments for governance.
