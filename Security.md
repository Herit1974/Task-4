# Amazon VPC Security 

---

## Data Protection in Amazon VPC
- **Shared Responsibility Model**: AWS secures the cloud infrastructure; you configure security for your resources.
- **Recommended Practices**:
  - Use **multi-factor authentication (MFA)**.
  - Enforce **TLS 1.2 or higher**.
  - Enable **AWS CloudTrail** for logging API activity.
  - Use **encryption solutions** and services like **Amazon Macie**.
  - Avoid placing sensitive data in tags or free-form text fields.

---

## Identity and Access Management (IAM)
- **Roles of IAM**:
  - Manage **authentication** (signing in).
  - Control **authorization** (who can do what).
- **IAM Components**:
  - **Users**: Long-term credentials (discouraged in favor of temporary credentials).
  - **Groups**: Collections of users.
  - **Roles**: Assignable, temporary credentials.
- **Policies**:
  - **Identity-based**: Attached to users, groups, or roles.
  - **Resource-based**: Attached directly to resources.
  - **Other Types**: SCPs, RCPs, permissions boundaries, session policies.
- **Best Practice**:
  - **Least privilege principle**: Grant only necessary permissions.

---

## Infrastructure Security
- **VPC Isolation**:
  - Each VPC is a logically isolated network.
  - Use **subnets** to segment resources by tier or function.
  - **PrivateLink** enables private connectivity to AWS services.
- **Traffic Control**:
  - **Security Groups**: Stateful, instance-level filtering.
  - **Network ACLs**: Stateless, subnet-level filtering.
  - **Route Tables**: Define network paths.
- **Secure Connectivity**:
  - Use **VPN** or **Direct Connect** for private links to your VPC.
  - **AWS Network Firewall** protects against threats.
  - **Flow Logs** monitor network traffic.
  - **Security Hub** helps identify misconfigurations.
- **Encryption & Signing**:
  - All requests must use **TLS** and be signed via **access keys** or **STS tokens**.

---

## Security Groups
- **Purpose**: Virtual firewalls controlling inbound and outbound traffic **at the instance level**.
- **Characteristics**:
  - **Stateful**: Return traffic automatically allowed.
  - Supports multiple security groups per resource.
  - No filtering of traffic to:
    - AWS DNS, DHCP, Metadata, License Activation, Time Sync.
- **Best Practices**:
  - Use **specific IP ranges** for SSH/RDP.
  - **Minimize open ports** and avoid 0.0.0.0/0 unless necessary.
  - Combine with NACLs for defense-in-depth.
  - Restrict who can create or modify security groups.
- **No additional cost** for security groups.

---

## Network ACLs
- **Purpose**: Subnet-level stateless traffic control.
- **Characteristics**:
  - **Stateless**: Must define rules for both inbound and outbound traffic.
  - Rules are evaluated in order by rule number (lowest to highest).
  - Default ACL allows all traffic.
  - Cannot block:
    - AWS DNS, DHCP, Metadata, etc.
- **Best Practices**:
  - Use to **complement security groups**.
  - Leave **gaps in rule numbering** for future updates.
  - Combine with **Route 53 Resolver DNS Firewall** for DNS filtering.

---

## Monitoring and Auditing
- **VPC Flow Logs**: Capture network traffic metadata.
- **Traffic Mirroring**: Copy packets for inspection.
- **Reachability Analyzer**: Visualize connectivity paths.
- **Network Access Analyzer**: Evaluate access paths to resources.
- **AWS CloudTrail**: Log all API calls.
- **AWS Security Hub**: Aggregate findings and compliance checks.
