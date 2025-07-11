# IP Addressing for VPCs and Subnets

Amazon VPC provides flexible options to assign and manage IPv4 and IPv6 addresses for your resources.

---

## IP Addressing Overview

- **CIDR Notation** defines IP ranges:
  - IPv4 example: `10.0.0.0/16` (65,536 addresses)
  - IPv6 example: `2001:db8:1234:1a00::/56` (massive address space)

---

## Private IPv4 Addresses

- **Private IPs** are not reachable over the internet.
- Assigned automatically when launching an instance.
- Each instance gets a private DNS name resolving internally.
- **Primary Private IP:**
  - Attached to the instance for its lifetime.
- **Secondary Private IPs:**
  - Can be reassigned between interfaces.
- Even if you use publicly routable CIDR blocks, direct internet access is **not supported** without a gateway:
  - Internet Gateway
  - NAT Gateway
  - VPN
  - Direct Connect

---

## Public IPv4 Addresses

- Subnets can auto-assign public IPs at launch.
- Public IP is mapped to private IP via NAT.
- **Released when unassigned** unless you use Elastic IPs.
- **Elastic IP (EIP):**
  - Persistent public IP owned by your account.
  - Can be associated/disassociated at will.
- **Charges apply** for all public IPv4 addresses, including EIPs.
- **DNS:**
  - Public DNS names resolve externally to public IP.
  - Internally resolve to private IP.

---

## IPv6 Addresses

- Larger address space than IPv4.
- Many AWS services support IPv6 (EC2, S3, CloudFront).
- Can be **dual-stack** or IPv6-only.

### Public IPv6 Addresses

- Always globally routable on the internet.
- Assigned automatically or via your own IPv6 range (BYOIP).
- Managed via:
  - Subnet CIDR blocks
  - Routing
  - Security Groups / Network ACLs

---

### Private IPv6 Addresses

- Not advertised on the internet.
- **Private IPv6 ULA:**
  - Start with `fd` (RFC4193).
  - Example range: `fd00::/8`.
- **Private IPv6 GUA:**
  - Must be owned by you.
  - Disabled by default (enable via IPAM).
- **Key Properties:**
  - Never routed to the internet.
  - AWS drops traffic at the internet gateway edge.
  - No extra cost.
  - AWS reserves the first 4 and last addresses in each subnet.
  - Communication across Direct Connect, VPN, Transit Gateway is allowed.

---

## IP Address Manager (IPAM)

- Create and manage pools of public/private IPv4/IPv6 addresses.
- Allocate contiguous address ranges.
- Monitor and track usage centrally.

---
