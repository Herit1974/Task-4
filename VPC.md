# Amazon Virtual Private Cloud (Amazon VPC)

Amazon VPC lets you launch AWS resources into a **logically isolated virtual network** that you define. This network is similar to an on-premises network but leverages AWS’s scalable infrastructure.

---

## Key Features

- **Virtual Private Clouds (VPC):** Your private network in AWS.
- **Subnets:** Segments of IP addresses within a VPC (must be in a single Availability Zone).
- **IP Addressing:**
  - Supports IPv4 and IPv6.
  - You can bring your own IP addresses.
- **Routing:**
  - Route tables control traffic flow within and outside the VPC.
- **Gateways & Endpoints:**
  - **Internet Gateway:** Enables internet access.
  - **NAT Gateway:** For outbound internet access from private subnets.
  - **VPC Endpoints:** Private connections to AWS services without internet exposure.
- **Peering Connections:** Connect VPCs privately.
- **Transit Gateways:** Central hub to connect multiple VPCs and on-premises networks.
- **Traffic Mirroring:** Copy network traffic for monitoring or security.
- **VPC Flow Logs:** Capture metadata about network traffic.
- **VPN Connections:** Securely link VPC to on-premises networks.

---

- Each AWS account has a **default VPC** in every AWS Region.
- You can create custom VPCs with your own configuration (subnets, routing, gateways).

---

## Management Options

- **AWS Management Console:** Web interface.
- **AWS CLI:** Command-line access.
- **AWS SDKs:** Language-specific APIs.
- **Query API:** Low-level HTTPS requests.

---

## Pricing Highlights

- **VPC creation/use:** No additional charge.
- **Charged components:**
  - NAT Gateways
  - Elastic IPs
  - Traffic Mirroring
  - Public IPv4 addresses (beyond Free Tier)
  - Some network analysis tools (e.g., Reachability Analyzer)

**Note:** AWS Free Tier includes **750 hours per month** of public IPv4 addresses with EC2.

---

## Public IPv4 Address Types

- **Elastic IP addresses (EIPs):** Static public IPs you can assign.
- **EC2 public IPv4 addresses:** Automatically assigned when instances launch.
- **BYOIP:** Bring Your Own public IPv4 addresses.
- **Service-managed public IPv4 addresses:** Provisioned automatically (e.g., ECS, RDS).

---
