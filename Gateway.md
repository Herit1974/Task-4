## Internet Gateway and Gateway Route Tables in AWS VPC

---

### Internet Gateway Overview
- A horizontally scaled, highly available VPC component that enables communication between your VPC and the internet.
- Supports IPv4 and IPv6 traffic.
- No extra charge to create or attach (standard EC2 data transfer charges apply).
- Provides a target in VPC route tables for internet-bound traffic.
- For IPv4, performs one-to-one NAT between private and public IPs or Elastic IPs.
- For IPv6, globally unique addresses are public by default (no NAT required).

---

### Subnet Internet Access
- **Public Subnet**: Has a route to the internet gateway (for example, 0.0.0.0/0 for IPv4).
- **Private Subnet**: No route to the internet gateway; no direct internet access even if instances have public IPs.
- **IP Requirements:**
  - IPv4: Instance must have a public IPv4 address or Elastic IP.
  - IPv6: VPC and subnet must have an IPv6 CIDR block, and the instance must have an IPv6 address.

---

### Defaults by VPC Type

| Feature                                       | Default VPC            | Nondefault VPC        |
|-----------------------------------------------|-------------------------|------------------------|
| Internet Gateway attached                    | Yes                     | No                     |
| Route to IGW for IPv4 (0.0.0.0/0)             | Yes                     | No                     |
| Route to IGW for IPv6 (::/0)                  | No                      | No                     |
| Auto-assign public IPv4                       | Yes (default subnet)    | No                     |
| Auto-assign IPv6                              | No                      | No                     |

---

### Gateway Route Tables
- A route table associated with an internet gateway or virtual private gateway.
- Used to control and intercept incoming VPC traffic (for example, redirect to security appliances).

Supported Route Targets:
- Local route (default).
- Gateway Load Balancer endpoint.
- Network interface of a middlebox appliance.

Destinations Allowed:
- Entire IPv4 or IPv6 CIDR of your VPC.
- Specific subnet CIDR within your VPC.

Rules and Considerations:
- Cannot contain routes to CIDR blocks outside your VPC.
- Only local, Gateway Load Balancer endpoint, or network interface targets are permitted.
- No prefix lists or other targets supported.
- Asymmetric routing is not supported; return traffic must pass through the same appliance.
- The middlebox network interface must be attached to a running instance (and must have a public IP for internet-bound traffic).
