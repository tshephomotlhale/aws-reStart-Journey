# AWS Networking

## Core Concepts & Keywords

- **VPC** – A logically isolated section of the AWS Cloud where you can launch resources.
- **Route Tables** – Determines where network traffic from the subnets is directed.
- **Internet Gateway (IGW)** – Enables access to the internet from your VPC.
- **NACL (Network ACLs)** – Acts as a firewall at the subnet level.
- **Security Groups** – Act as a firewall at the instance level.
- **Subnets** – Logical partition of an IP network into multiple smaller network segments.
- **Availability Zone (AZ)** – A single data center within an AWS Region.
- **Region** – The geographical location of your AWS infrastructure.
- **AWS VPN** – Secure connection between on-premises, remote offices, and AWS.
- **AWS Direct Connect** – Dedicated physical connection from your data center to AWS (like a private fiber cable).
- **PrivateLink (VPC Interface Endpoints)** – Privately connect to AWS services or third-party apps without traversing the public internet.
- **AWS Transit Gateway** – A central **hub** to connect multiple VPCs and on-premises networks (“router in the cloud”).

---

## Virtual Private Cloud (VPC) & Subnets

<figure>
  <img src="/public/VPC.png" alt="VPC showing public and private subnets with an internet gateway" width="200" />
  <figcaption><em>VPC with public/private subnets and Internet Gateway</em></figcaption>
</figure>

- **VPC**
    - Logically isolated section of AWS where you launch resources.
    - You choose a CIDR Range (e.g., `10.0.0.0/16` → 65,536 IPs).
    - Think of it like your **digital neighborhood**.
- **Subnets**
    - Logical partition of the VPC CIDR range.
    - **Public Subnet** → Can access internet (via Internet Gateway).
    - **Private Subnet** → No direct internet access.
- **Route Tables**
    - Rules that determine traffic direction.
    - **Destination** (where traffic goes) + **Target** (how it gets there).
- **Internet Gateway (IGW)**
    - Enables internet access for resources in public subnets.
- **NAT Gateway/Instance**
    - Allows private subnet instances to access the internet without being exposed.
- **VPC Flow Logs**
    - Capture traffic details (diagnostics, monitoring, troubleshooting).
- **VPC Peering**
    - Private communication between two VPCs (IPv4/IPv6).
- **VPC Endpoints (via PrivateLink)**
    - Private connections to AWS services without using the public internet.

### Exam Tips
- VPC is **region-specific**, and subnets are **AZ-specific**.
- NAT Gateway is **managed** (scales, HA) → use in exams unless asked about cost.
- **VPC Flow Logs** don’t capture packet content, only metadata.
- **Peering** is 1-to-1, **Transit Gateway** is for many-to-many.

---

## Security Groups vs NACLs

| **Characteristic** | **Security Groups** | **NACLs** |
|----------------------|----------------------|-----------|
| **Level**           | Instance level       | Subnet level |
| **Scope**           | Applied to instances with that SG | Applied to all instances in the subnet |
| **Rules**           | Only **ALLOW** rules | **ALLOW + DENY** rules |
| **Evaluation**      | Checks all rules     | Checked in order (lowest → highest) |
| **Return traffic**  | Allowed automatically (**stateful**) | Must be explicitly allowed (**stateless**) |

### Exam Tips
- **Security Groups** = Stateful, allow-only.
- **NACLs** = Stateless, allow + deny.
- Block IPs? Use **NACLs**.
- Allow port 22 SSH to EC2? Use **Security Groups**.

---

## AWS VPN
<figure>
  <img src="/public/ClientVPN.png" alt="Client Virtual Private Network" width="200" />
  <figcaption><em>Client Virtual Private Network</em></figcaption>
</figure>
<figure>
  <img src="/public/SitetoSiteVPN.png" alt="Site to Site Virtual Private Network" width="200" />
  <figcaption><em>Site to Site  Virtual Private Network</em></figcaption>
</figure>
- **Purpose** → Secure connections between on-premises, remote workers, and AWS.

### Types
- **Site-to-Site VPN**
    - Connects on-premises network (data center, office LAN) to an AWS VPC.
    - Network-to-network connection.
- **Client VPN**
    - Remote users connect securely via OpenVPN.
    - User-to-network connection.

### Exam Tips
- **Site-to-Site VPN** → Network ↔ Network.
- **Client VPN** → User ↔ Network.
- Low-latency, high-throughput hybrid → **Direct Connect**, not VPN.

---

## AWS Direct Connect
<figure>
  <img src="/public/DirectConnect.png" alt="AWS DirectConnect" width="200" />
  <figcaption><em>AWS DirectConnect</em></figcaption>
</figure>

- **What it is** → Dedicated, private physical connection from your data center to AWS.
- **Use Case** → Hybrid cloud setups needing fast, consistent, low-latency connections.
- **Think of it as**: A **private fiber cable** to AWS.

### Exam Tips
- If question mentions **private, dedicated, consistent bandwidth** → **Direct Connect**.
- VPN = internet-based, cheaper but less reliable.

---

## PrivateLink (VPC Interface Endpoints)
<figure>
  <img src="/public/PrivateLink.png" alt="PrivateLink" width="200" />
  <figcaption><em>PrivateLink</em></figcaption>
</figure>

- **What it is** → Private connections to AWS services or SaaS apps using the AWS backbone.
- **Think of it as**: A **private doorway inside your VPC** to AWS services.

### Exam Tips
- If question says “**keep traffic off the internet**” → **PrivateLink**.
- Unlike VPC Peering, PrivateLink is **service-based**, not VPC-to-VPC.

---

## AWS Transit Gateway
<figure>
  <img src="/public/TransitGateway.png" alt="AWS TransitGateway" width="200" />
  <figcaption><em>AWS TransitGateway</em></figcaption>
</figure>

- **What it is** → A hub for connecting multiple VPCs and on-prem networks.
- **Think of it as** → A **cloud router** that simplifies complex networking.

### Exam Tips
- Many VPCs need interconnectivity? → **Transit Gateway**.
- For simple 1-to-1 VPC connection → **Peering**.

---

## AWS Global Accelerator
<figure>
  <img src="/public/GlobalAccelerator.png" alt="AWS Global Accelerator" width="200" />
  <figcaption><em>AWS Global Accelerator</em></figcaption>
</figure>

- **What it is** → A service that routes traffic via AWS’s **private global network** instead of the public internet.
- Provides **two static anycast IPs**.
- Improves:
    - **Availability** → reroutes away from unhealthy endpoints.
    - **Performance** → routes to closest/fastest region.
    - **Consistency** → static entry point.

### Types
- **Standard Accelerator** → Routes to closest healthy AWS endpoint.
- **Custom Routing Accelerator** → Fine-grained control (user IP/port mapping → specific destination).

### Exam Tips
- “**Two static IPs, global optimization, performance, failover**” = **Global Accelerator**.
- Don’t confuse with **CloudFront**:
    - CloudFront = **content delivery** (HTTP/HTTPS).
    - Global Accelerator = **global app performance** (TCP/UDP).

---

## Content Delivery Network (CDN) – Amazon CloudFront
<figure>
  <img src="/public/CloudFront.png" alt="Amazon CloudFront" width="200" />
  <figcaption><em>Amazon CloudFront</em></figcaption>
</figure>

- **Purpose** → Distribute content via **edge locations** for faster delivery.
- Uses **caching, acceleration, and edge logic**.

### Use Cases
- Websites & web apps.
- Video streaming.
- APIs & dynamic content.
- Large file/software distribution.

### CloudFront vs Global Accelerator

| **CloudFront** | **Global Accelerator** |
|----------------|------------------------|
| Delivers web content | Improves app performance globally |
| HTTP/HTTPS only | TCP/UDP |
| Caches content | Routes live traffic |

### Exam Tips
- CloudFront = **Content delivery**.
- Global Accelerator = **Global app traffic optimization**.

---

## Amazon Route 53
<figure>
  <img src="/public/Route53.png" alt="Amazon Route 53" width="200" />
  <figcaption><em>Amazon Route 53</em></figcaption>
</figure>

- **DNS Service** – translates domain names into IPs.
- **Features**
    - Domain registration.
    - DNS routing (A, AAAA, CNAME, Alias, etc.).
    - Health checks + failover.
    - Integrates with CloudFront, ELB, S3, API Gateway.

### Routing Policies
- **Simple** → One record → One resource.
- **Weighted** → Split traffic (A/B testing).
- **Latency-based** → Send to lowest-latency region.
- **Failover** → Primary/secondary for DR.

### Exam Tips
- “**DNS, port 53, routing policies**” → Route 53.
- Alias records support AWS resources (Apex domains → CloudFront/S3).

---

## Elastic Load Balancer (ELB)
<figure>
  <img src="/public/ELB.png" alt="Amazon Elastic Load Balancer" width="200" />
  <figcaption><em>Amazon Elastic Load Balancer</em></figcaption>
</figure>

- **Purpose** → Distributes traffic across multiple targets (EC2, containers, IPs, Lambda).
- Ensures **availability, scalability, and fault tolerance**.

### Types
- **Application Load Balancer (ALB)** → Layer 7 (HTTP/HTTPS, microservices, routing).
- **Network Load Balancer (NLB)** → Layer 4 (TCP/UDP/TLS, ultra-low latency).
- **Gateway Load Balancer (GWLB)** → Deploy 3rd-party firewalls/security appliances.
- **Classic Load Balancer (CLB)** → Legacy, basic Layer 4 & 7.

### Exam Tips
- Layer 7? → **ALB**.
- High-performance TCP/UDP? → **NLB**.
- Security appliances? → **GWLB**.
- Old exam question? Might mention **CLB** (legacy).

---
