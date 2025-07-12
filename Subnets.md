# Subnets

**Definition:**
A subnet is a range of IP addresses within your VPC where you deploy resources.

**Subnet Types:**
- **Public Subnet:** Has a route to an Internet Gateway.
- **Private Subnet:** No direct route to the Internet; uses a NAT device.
- **VPN-only Subnet:** Routes traffic through a Site-to-Site VPN.
- **Isolated Subnet:** No outbound routes; internal-only communication.

**Subnet IP Addressing:**
- **IPv4 Only:** IPv4 addresses only.
- **Dual Stack:** IPv4 and IPv6.
- **IPv6 Only:** IPv6 addresses only (uses IPv4 link-local addresses internally).

**Subnet Routing:**
- Every subnet must be associated with a **route table**.
- Default: Subnets use the **main route table** unless explicitly associated with another.
- Each subnet can only be linked to one route table at a time.

**Subnet Settings:**
- **Auto-assign public IPs:** Enable/disable automatic assignment.
- **Resource-based Name (RBN):** Control instance DNS names.

**Security:**
- Use **private subnets** and **NAT/bastion hosts** for secure internet access.
- **Security Groups:** Instance-level traffic control.
- **Network ACLs:** Subnet-level traffic control.
- **Flow Logs:** Capture subnet or interface traffic.

---

# Route Table Concepts

**Main Route Table:**
- Created automatically with the VPC.
- Used by all subnets without explicit associations.
- Can be edited but **not deleted**.

**Custom Route Table:**
- Created manually.
- Allows custom routing logic.
- Can be associated explicitly with subnets.

**Key Terms:**
- **Destination:** The CIDR block traffic is routed to.
- **Target:** The device/gateway handling the traffic.
- **Local Route:** Always exists for VPC internal traffic.
- **Propagation:** Auto-updates VPN routes if enabled.
- **Edge Association:** Routing inbound traffic to appliances.
- **Transit Gateway Route Table:** For VPC transit gateways.
- **Local Gateway Route Table:** Used in AWS Outposts.

---

# Subnet Route Tables

**Basics:**
- Each subnet is associated with one route table.
- **Implicit Association:** Defaults to the main route table.
- **Explicit Association:** Linked to a custom route table.
- Multiple subnets can share the same route table.

**Routes:**
- Each route defines:
  - **Destination:** CIDR range.
  - **Target:** Internet Gateway, NAT Gateway, Peering Connection, etc.
- IPv4 and IPv6 routes are configured separately.
- **Longest prefix match** determines routing precedence.
- Reserved ranges (`169.254.168.0/22`, `fd00:ec2::/32`) cannot be routed.

**Main Route Table Rules:**
- Can't delete the main route table.
- You can replace it with a custom table.
- You can explicitly associate subnets back to the main table.

**Example Usage:**
- **Public subnet:** Route `0.0.0.0/0` to Internet Gateway.
- **Private subnet:** Route traffic through NAT Gateway or VPN.
- **Replacing Main Table:** Test routing with a custom table before replacing.

---

