# NAT devices

## NAT Gateways

A **NAT gateway** enables instances in a **private subnet** to access the internet (or other AWS services) without allowing inbound connections from the internet. It is a **managed service** that scales automatically.

### Types
- **Public NAT Gateway**
  - Placed in a **public subnet**.
  - Requires an **Elastic IP address**.
  - Routes internet-bound traffic through the internet gateway.
  - Enables private subnet instances to access the internet.

- **Private NAT Gateway**
  - Placed in a **private subnet**.
  - Does **not** associate an Elastic IP.
  - Routes traffic to other VPCs or on-premises networks via a **transit gateway** or **virtual private gateway**.
  - Cannot send traffic to the internet.

### Key Characteristics
- Supports **IPv4 and IPv6** (IPv6 via DNS64/NAT64).
- Each IPv4 address on a NAT gateway supports up to **55,000 concurrent connections to a unique destination**.
- You can associate up to:
  - **8 private IPv4 addresses** (1 primary + 7 secondary) for a private NAT gateway.
  - **2 Elastic IPs** for a public NAT gateway (default quota).
- You **pay per hour and per GB of traffic** processed.

### Management Tasks
- Create and tag NAT gateways.
- Add or remove secondary IP addresses to increase port availability.
- Monitor metrics like:
  - `ErrorPortAllocation` (port exhaustion).
  - `PacketsDropCount` (dropped packets).
- Update route tables to point `0.0.0.0/0` to the NAT gateway.

---

## NAT Instances

A **NAT instance** is a self-managed EC2 instance configured to perform NAT for private subnet resources.

### When to Use
- You need **custom configurations** (e.g., special firewall rules or software).
- **Cost-sensitive workloads** with low bandwidth requirements.
- You understand and accept the operational overhead.

### Key Characteristics
- Must be launched in a **public subnet** with a **public IP/Elastic IP**.
- Requires **source/destination checks disabled**.
- **Does not auto-scale**—you must resize or replace it yourself.
- AWS recommends migrating to NAT gateways, as NAT instances use an **old Amazon Linux AMI (2018.03)** which has reached end of life.

---

## NAT Instance Setup Workflow

1. **Create a VPC**
   - Includes both public and private subnets.

2. **Create a Security Group**
   - Inbound: allow HTTP/HTTPS from private subnet, SSH from your network.
   - Outbound: allow HTTP/HTTPS to the internet.

3. **Create a NAT AMI**
   - Launch EC2 with Amazon Linux 2 or AL2023.
   - Enable **IP forwarding** (`net.ipv4.ip_forward=1`).
   - Configure **iptables** NAT rules
   - Create an AMI.

4. **Launch the NAT Instance**
   - Use the NAT AMI.
   - Place it in the **public subnet**.
   - Enable auto-assign public IP.
   - Attach the security group.

5. **Disable Source/Destination Checks**
   - Required so it can forward traffic.

6. **Update Route Table**
   - Add route: `0.0.0.0/0` pointing to the NAT instance ID.

7. **Test Connectivity**
   - SSH into the private instance and test internet access.

---

## Comparison: NAT Gateway vs. NAT Instance

| Feature               | NAT Gateway                     | NAT Instance                        |
|-----------------------|---------------------------------|--------------------------------------|
| Management            | Fully managed                  | Self-managed                        |
| Scalability           | Auto-scales                    | Must resize manually                |
| Availability          | Highly available               | Single point of failure (unless HA) |
| Bandwidth             | 5–45 Gbps                      | Depends on instance type            |
| Cost                  | Higher                         | Potentially lower                   |
| Customization         | Limited                        | Full OS-level customization         |
| Recommended?          | Yes (modern workloads)         | Use only if customization needed    |

---
