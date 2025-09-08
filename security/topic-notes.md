# AWS Security Services

# AWS IAM (Identity and Access Management)

**Definition:** It is an AWS web service that helps you securely control who can access your AWS resources and what actions they can perform.

- It a security service that control access to resources and services.
- You can create Groups, Users and Roles then assign fine-grained permissions to define what they are allowed to access in your AWS env.
- It focuses on Authentication (signed in) and Authorization (has permissions).

**IAM Elements**

- **Principal** – The **who**.
    
    The entity (user, role, service, application) that makes a request to AWS resources.
    
- **Request** – The **attempt**.
    
    The action the principal wants to perform, like “read an S3 object.”, “use AWS Management Console”
    
- **Authentication** – The **proof**.
    
    Verifying the principal’s identity (e.g., password, access keys, MFA).
    
- **Authorization** – The **check**.
    
    Decides if the authenticated principal has permission to do the requested action.
    
- **Actions and Operations** – The **what**.
    
    The specific subset of actions within a service that the permission allows or denies.
    
- **Resources** – The **where**.
    
    The AWS object the action applies to, like an S3 bucket, EC2 instance, or DynamoDB table.
    

**IAM Identities**

- **AWS Root Account User**
    - The original account created when you sign up for AWS.
    - Has **unrestricted access** to everything.
    - Best practice → lock it down, use MFA, and don’t use it daily.
- **IAM User**
    - A person or application with **credentials** (username/password or access keys).
    - Used for regular access.
- **IAM Group**
    - A collection of users.
    - Permissions assigned to the group apply to all members.
- **IAM Role**
    - A **temporary identity** with specific permissions.
    - Assumed by users, AWS services (like EC2), or apps.
    - No long-term credentials.
- **IAM Policies**
    - JSON documents that define **what actions** are allowed/denied on **which resources**.
    - Attached to **users, groups, or roles**.
- **IAM Policy Inheritance**
    - Users inherit all permissions from **groups** they belong to and policies attached to them.
    - Effective permissions = **sum of everything**, unless there’s an explicit **Deny**.
- **IAM Password Policy**
    - Defines rules for user passwords (length, complexity, expiration).
    - Helps improve account security.
- **MFA (Multi-Factor Authentication)**
    - Extra layer of security → requires **something you know** (password) + **something you have** (MFA code/device).

**How User Access AWS**

- **AWS Management Console**
    - Web-based UI for humans (sign in via browser).
    - **Protected by:**
        - Username + Password
        - (Best practice) **MFA** for extra security
- **AWS Command Line Interface (CLI)**
    - Tool for running AWS commands from a terminal.
    - **Protected by:**
        - **Access Keys** (Access Key ID + Secret Access Key)
- **AWS SDK (Software Development Kit)**
    - For developers to call AWS services from code (Python, Java, Node.js, etc.).
    - **Protected by:**
        - **Access Keys** (programmatically stored/used)

**Security Tools**

- IAM Credentials Report (account-level) : 
Shows the **status of credentials** (passwords, access keys, MFA) for all IAM users.
- IAM Access Advisor (user-level): 
Shows **which AWS services** the user/role has **permissions to access** and **when they were last accessed**.

# Amazon CloudWatch

**Definition:** Amazon CloudWatch is a **monitoring and observability service** for AWS resources, applications, and services.

- Collects **metrics** (numbers) about your AWS services (CPU, memory, requests, latency).
- Collects **logs** (text output) from your apps and services.
- Lets you create **alarms** to act when something goes wrong.
- Provides **dashboards** to visualize health and performance.
- Helps with **automated responses** (like scaling up EC2 when load increases).

- **M** → Metrics → Numbers
- **L** → Logs → Records
- **A** → Alarms → Reactions
- **D** → Dashboards → Visuals

**Features:**

- **CloudWatch Metrics**
    - Numerical data points (CPU %, latency, disk I/O, custom metrics).
    - Used to measure performance.
- **CloudWatch Logs**
    
    A service that collects, monitors, and stores **log data** from AWS resources, applications, or on-prem servers.
    
    **What does it do?**
    
    - Stores logs from services like **EC2, Lambda, RDS, VPC Flow Logs**.
    - Lets you **search, filter, and analyze** logs.
    - Can stream logs to **S3** (for storage) or **Elasticsearch/OpenSearch** (for analysis).
- **CloudWatch Alarms:** A **CloudWatch Alarm** watches a metric (like CPU usage, memory, or custom metrics) and **performs an action** when a threshold is breached. used to trigger a notification
    
    **What does it do?**
    
    - Monitors metrics in **real-time**.
    - Triggers actions like:
        - Send an **SNS notification** (email, SMS).
        - **Auto scale** an EC2 instance.
        - **Stop, reboot, or terminate** an instance.
- **CloudWatch Dashboards**
    - Custom visual boards to monitor metrics in real-time.
- **CloudWatch Events / EventBridge**
    - Responds to system events (e.g., start a Lambda when an EC2 state changes).
- **CloudWatch Contributor Insights**
    - Identifies top contributors to a metric (e.g., which IP causes most requests)

# Amazon CloudTrail

**Definition:** It is a logging and auditing service that keeps track of all actions or API calls that can happen in your AWS Account, it enables you to create , it enables operational and risk auditing for young your account.

- who made the request
- what action they performed
- when the action occurred
- which resources were affected

**Importance**

- Security
- Compliance
- Troubleshooting
- Auditing

# AWS Shield

**Definition:**
AWS Shield is a **fully managed Distributed Denial of Service (DDoS) protection service** that safeguards AWS applications from DDoS attacks automatically.

**What is DDoS:** 

- Cyberattack where attackers **flood a server with massive fake traffic**, overwhelming resources and making the service **unavailable** to real users.
- Think of it like **a traffic jam** on the internet highway → nobody can get through.

**How it works:**

- **Traffic Monitoring** – Continuously monitors incoming traffic to AWS applications.
- **Detection** – Identifies abnormal traffic spikes or malicious patterns.
- **Mitigation** – Filters out malicious traffic while letting legitimate requests through.
- **Integration** – Works with **Amazon CloudFront, Route 53, and Elastic Load Balancer** for best protection.

**How to identify a DDoS Attack**

- Sudden **spike in requests** from many IPs.
- Website/service becomes **slow or unreachable**.
- Unusual **network traffic patterns**.
- AWS monitoring tools (like **CloudWatch metrics**) showing abnormal usage.

**Tiers of AWS Shield**

- **AWS Shield Standard (Free, automatic)**
    - Provides protection against common **Layer 3 & 4 attacks** (e.g., SYN/UDP floods, reflection attacks).
    - Automatically included with CloudFront, Route 53, ALB, etc.
    - Good for most applications.
- **AWS Shield Advanced (Paid, premium)**
    - Extra protection for more **sophisticated & larger-scale DDoS attacks**.
    - 24/7 access to the **AWS DDoS Response Team (DRT)**.
    - **Cost protection** → helps with unexpected scaling charges from DDoS.
    - Real-time attack visibility + detailed reporting.
    - Integrates with **AWS WAF** for custom filtering.

Benefits

- **Always-on protection** (automatic with Shield Standard).
- **Minimizes downtime** → keeps apps available during attacks.
- **Scalable defense** → handles very large DDoS attacks.
- **Integration** with AWS services (CloudFront, Route 53, ELB, WAF).
- **Cost protection** with Shield Advanced (prevents surprise bills).
- **Expert support** via AWS DDoS Response Team.

# Amazon Guard Duty

**Definition:** 

Amazon Guard Duty is a **threat detection service** that continuously monitors AWS accounts, workloads, and data for **malicious or unauthorized behavior**.

It uses **machine learning, anomaly detection, and threat intelligence** to detect security risks.

- **Data Sources** → Guard Duty analyzes:
    - **VPC Flow Logs** (network traffic).
    - **CloudTrail Logs** (API activity).
    - **DNS Logs** (domain lookups).
- **Analysis** → Uses ML + AWS threat intelligence to detect anomalies.
- **Findings** → Provides alerts with severity (Low, Medium, High).
- **Response** → You can automate responses (e.g., isolate EC2 instances, revoke keys) using **EventBridge + Lambda**.

**Benefits:**

- Improves **security visibility** across AWS.
- Helps detect attacks like **crypto-mining, account compromise, reconnaissance**.
- **No infrastructure to manage** (serverless).
- Supports **automated incident response**.
- Provides **actionable insights** instead of raw logs.

# Amazon Inspector

**Definition:**
Amazon Inspector is an **automated vulnerability management service** that scans AWS workloads (like **EC2 instances, ECR container images, and Lambda functions**) for **software vulnerabilities and unintended network exposure**.

**How it works:**

- **Automatic discovery** of supported resources (EC2, ECR, Lambda).
- **Continuous scanning** → no need for manual scheduling.
- **Assessment rules** → uses AWS + industry vulnerability databases (like NVD).
- **Findings generated** with severity (Critical, High, Medium, Low).
- **Remediation guidance** provided (e.g., update to patched version).

# Amazon Trusted Advisor

**Definition:**

Amazon Trusted Advisor is an **AWS service that provides real-time guidance to help you provision your resources following AWS best practices** It **analyzes your AWS environment** and gives recommendations to improve **cost optimization, security, performance, and fault tolerance**

**Features:**

- **Cost Optimization Checks** → Identify idle or underutilized resources.
- **Security Checks** → Detect overly permissive IAM policies, exposed ports, or lack of MFA.
- **Fault Tolerance Checks** → Ensure redundancy and backup configurations.
- **Performance Checks** → Spot resource bottlenecks or suboptimal configurations.
- **Service Limits Checks** → Alerts when approaching AWS service limits.
- **Accessible via Console, API, and CLI** → Automate checks and reporting.

# AWS Network Firewall

**Definition:**

AWS Network Firewall is a **managed network security service** that makes it easy to **deploy essential protections for your Amazon Virtual Private Clouds (VPCs)** It helps **control and monitor traffic** at the network level to prevent unauthorized access and threats.

- It provides fine-grained network traffic control that allows you to restrict outbound requests prevent malicious activity from spreading

**Benefits**

- **Simplified network security** → No need to manage your own firewall appliances.
- **Customizable rules** → Tailor protections to your network needs.
- **Scalable** → Automatically scales to handle traffic volume.
- **Centralized management** → With Firewall Manager, manage multiple VPCs easily.
- **Enhanced compliance** → Helps meet regulatory and security requirements.

# AWS Firewall Manager

**Definition:**

- A **centralized security management service** in AWS.
- Helps **apply firewall rules across multiple AWS accounts and resources** consistently.
- Works with **AWS WAF, AWS Shield Advanced, and AWS Network Firewall, Route 53 Resolver**

**How it works**

- You define a **security policy** in Firewall Manager.
- That policy is automatically applied across:
    - **VPCs**
    - **Accounts in AWS Organizations**
    - **Resources like ALBs, CloudFront distributions, and VPCs**

**Key Features**

- **Centralized Management** – Instead of configuring WAF rules or firewall policies per resource, you manage them once and enforce everywhere.
- **Compliance Enforcement** – Ensures all new and existing resources comply with security rules (e.g., every ALB must have WAF rules).
- **Multi-account Protection** – Especially useful in large enterprises with **AWS Organizations**.

**Use Cases**

- Company with 20 AWS accounts wants to enforce WAF rules **on every CloudFront distribution**.
- Enforce **Shield Advanced** protections automatically on all internet-facing apps.
- Ensure every VPC uses **AWS Network Firewall policies**.

# Amazon WAF

**Definition:**

- A **layer 7 firewall** that protects **web applications** from common exploits.
- Works with **CloudFront, ALBs, API Gateway, and AppSync**.

**What it protects against:**

- **SQL Injection**
- **Cross-Site Scripting (XSS)**
- **HTTP Floods** (basic DDoS attempts)
- Custom rules using IP addresses, HTTP headers, geolocation, etc.

**How it works**

- You define **Web ACLs (Access Control Lists)**.
- Each Web ACL contains **rules** that either:
    - Allow traffic
    - Block traffic
    - Count (monitor only) traffic

**Key Features**

- **Rule sets**: AWS Managed Rules (prebuilt) + custom rules.
- **Rate limiting**: Block IPs that send too many requests.
- **Integration**: Protects CloudFront, ALB, API Gateway, AppSync.

**Use Cases**

- E-commerce website wants to block **SQL injection & XSS attacks**.
- API wants to allow only requests from **specific countries**.
- Blog wants to block **scrapers sending >1000 requests per min**

# Penetration Testing on AWS

**Definition**

- **Penetration Testing (pentesting)** = Simulating cyberattacks against your AWS environment to test security.
- Goal: Identify **vulnerabilities** before attackers do.

**AWS Rules for Pentesting**

AWS **allows pentesting**, but with **restrictions**:

1. **No need for prior approval anymore** (since 2019, AWS removed the pre-approval requirement for common tests).
2. Allowed testing includes:
    - EC2, RDS, CloudFront, API Gateway, Lambda, etc.
    - Testing your own resources only (never AWS-managed infra).
3. **Prohibited activities**:
    - Denial of Service (DoS) or Distributed DoS (DDoS) simulations.
    - Port flooding or protocol flooding.
    - DNS zone walking against Route53.
    - Attacks that affect other AWS customers.

**Best Practices**

- Always test **non-production environments first**.
- Use **AWS Inspector & Guard Duty** as automated tools before manual pentesting.
- Document and patch vulnerabilities found.

# Quiz

### **Question 1**

A company hosting a website on AWS wants automatic protection against DDoS attacks. Which service provides this?

Select one:

a. AWS GuardDuty

b. AWS Inspector

c. AWS WAF

d. AWS Shield Standard

---

### **Question 2**

A system administrator wants to visualize EC2 CPU usage in near real time. Which CloudWatch component is best suited?

Select one:

a. CloudWatch Logs

b. CloudWatch Dashboard

c. CloudTrail

d. CloudWatch Alarms

---

### **Question 3**

Which two types of metrics can CloudWatch collect? (Choose 2)

Select one or more:

a. IAM policies

b. Security group rules

c. Billing metrics

d. Custom metrics from applications

---

### **Question 4**

Which IAM entity can only contain permissions but cannot directly make requests to AWS services?

Select one:

a. IAM Group

b. IAM User

c. IAM Policy

d. IAM Role

---

### **Question 5**

Which AWS service provides best practice recommendations across cost, security, performance, and fault tolerance?

Select one:

a. Amazon GuardDuty

b. Amazon CloudTrail

c. Amazon Inspector

d. AWS Trusted Advisor

---

### **Question 6**

A compliance team wants to ensure EC2 instances are following security best practices. Which service provides automated security assessments?

Select one:

a. AWS Shield

b. Amazon GuardDuty

c. Amazon Inspector

d. Amazon CloudWatch

---

### **Question 7**

Which AWS service records all API calls made in your AWS account, including from the Management Console, CLI, and SDKs?

Select one:

a. Amazon CloudTrail

b. Trusted Advisor

c. Amazon GuardDuty

d. Amazon CloudWatch

---

### **Question 8**

A security team wants to identify who deleted an S3 bucket. Which service should they check?

Select one:

a. AWS Shield

b. Amazon GuardDuty

c. AWS CloudTrail

d. AWS Inspector

---

### **Question 9**

A security analyst needs to detect unusual API activity and potential compromised IAM credentials. Which service should they use?

Select one:

a. AWS Shield

b. AWS GuardDuty

c. AWS WAF

d. AWS Inspector

---

### **Question 10**

Which two resources can AWS WAF protect? (Choose 2)

Select one or more:

a. Application Load Balancers

b. IAM Roles

c. EC2 Instances directly

d. Amazon CloudFront distributions

---

### **Question 11**

Which two are key benefits of CloudTrail? (Choose 2)

Select one or more:

a. Real-time malware scanning

b. Monitoring API activity

c. Compliance and auditing

d. Protecting against DDoS attacks

---

### **Question 12**

Trusted Advisor checks can help with which of the following? (Choose 2)

Select one or more:

a. DDoS Mitigation

b. Real-time malware detection

c. Cost Optimization

d. Identity and Access Management

---

### **Question 13**

Which AWS service provides fine-grained network traffic filtering at the VPC level?

Select one:

a. AWS Network Firewall

b. AWS WAF

c. AWS Shield

d. CloudTrail

---

### **Question 14**

Which two data sources does GuardDuty analyze to detect threats? (Choose 2)

Select one or more:

a. CloudTrail Events

b. VPC Flow Logs

c. CloudWatch Dashboards

d. IAM Policies

---

### **Question 15**

A company wants to automatically restart an EC2 instance when CPU utilization is below 5% for 30 minutes. Which CloudWatch feature should they use?

Select one:

a. CloudTrail Events

b. CloudWatch Dashboards

c. CloudWatch Alarms

d. CloudWatch Logs

---

### **Question 16**

An organization wants to perform penetration testing on its AWS resources. What is the correct step before conducting the test?

Select one:

a. Disable CloudTrail

b. Deploy GuardDuty

c. Run Trusted Advisor checks

d. Contact AWS Support for authorization

---

### **Question 17**

What is the main difference between AWS Shield Standard and Shield Advanced?

Select one:

a. Shield Advanced replaces GuardDuty

b. Shield Advanced includes IAM support

c. Shield Advanced provides 24/7 DDoS response team access

d. Shield Standard is paid, Shield Advanced is free

---

### **Question 18**

A global company wants a single service to deploy WAF rules, Shield protections, and Network Firewall policies across multiple AWS accounts. Which service is most suitable?

Select one:

a. AWS Firewall Manager

b. AWS CloudWatch

c. AWS Trusted Advisor

d. Amazon Inspector

---

### **Question 19**

A developer needs temporary access keys to interact with AWS services for a few hours. Which IAM feature should be used?

Select one:

a. IAM Groups

b. IAM Roles

c. IAM Users

d. IAM Policies

---

### **Question 20**

Which AWS service automatically scans EC2 instances for software vulnerabilities and missing patches?

Select one:

a. AWS Shield

b. AWS Trusted Advisor

c. Amazon Inspector

d. AWS WAF

---

### **Question 21**

An e-commerce company wants to block SQL injection and cross-site scripting attacks on its website. Which service should they use?

Select one:

a. AWS WAF

b. AWS Shield

c. AWS Inspector

d. AWS GuardDuty

---

### **Question 22**

Which two AWS services require explicit approval for penetration testing? (Choose 2)

Select one or more:

a. Amazon Route53

b. Amazon RDS

c. AWS Lambda

d. Amazon CloudFront

---

### **Question 23**

A company wants to apply centralized firewall policies across multiple AWS accounts. Which service should they use?

Select one:

a. Amazon GuardDuty

b. AWS Network Firewall

c. AWS WAF

d. AWS Firewall Manager

---

### **Question 24**

Your organization wants to ensure developers follow least privilege principles. Which two IAM features help achieve this? (Choose 2)

Select one or more:

a. Amazon GuardDuty

b. IAM Policies

c. IAM Access Analyzer

d. AWS Shield

---

### **Question 25**

A company wants to test the resilience of their AWS applications by simulating cyberattacks. What is this process called?

Select one:

a. Security Patching

b. Intrusion Prevention

c. GuardDuty Analysis

d. Penetration Testing

### **Question 11**

Which two are key benefits of CloudTrail? (Choose 2)

Select one or more:

a. Real-time malware scanning

b. Monitoring API activity

c. Compliance and auditing

d. Protecting against DDoS attacks

---

### **Question 12**

Trusted Advisor checks can help with which of the following? (Choose 2)

Select one or more:

a. DDoS Mitigation

b. Real-time malware detection

c. Cost Optimization

d. Identity and Access Management

---

### **Question 13**

Which AWS service provides fine-grained network traffic filtering at the VPC level?

Select one:

a. AWS Network Firewall

b. AWS WAF

c. AWS Shield

d. CloudTrail

---

### **Question 14**

Which two data sources does GuardDuty analyze to detect threats? (Choose 2)

Select one or more:

a. CloudTrail Events

b. VPC Flow Logs

c. CloudWatch Dashboards

d. IAM Policies

---

### **Question 15**

A company wants to automatically restart an EC2 instance when CPU utilization is below 5% for 30 minutes. Which CloudWatch feature should they use?

Select one:

a. CloudTrail Events

b. CloudWatch Dashboards

c. CloudWatch Alarms

d. CloudWatch Logs

---

### **Question 16**

An organization wants to perform penetration testing on its AWS resources. What is the correct step before conducting the test?

Select one:

a. Disable CloudTrail

b. Deploy GuardDuty

c. Run Trusted Advisor checks

d. Contact AWS Support for authorization

---

### **Question 17**

What is the main difference between AWS Shield Standard and Shield Advanced?

Select one:

a. Shield Advanced replaces GuardDuty

b. Shield Advanced includes IAM support

c. Shield Advanced provides 24/7 DDoS response team access

d. Shield Standard is paid, Shield Advanced is free

---

### **Question 18**

A global company wants a single service to deploy WAF rules, Shield protections, and Network Firewall policies across multiple AWS accounts. Which service is most suitable?

Select one:

a. AWS Firewall Manager

b. AWS CloudWatch

c. AWS Trusted Advisor

d. Amazon Inspector

---

### **Question 19**

A developer needs temporary access keys to interact with AWS services for a few hours. Which IAM feature should be used?

Select one:

a. IAM Groups

b. IAM Roles

c. IAM Users

d. IAM Policies

---

### **Question 20**

Which AWS service automatically scans EC2 instances for software vulnerabilities and missing patches?

Select one:

a. AWS Shield

b. AWS Trusted Advisor

c. Amazon Inspector

d. AWS WAF

---

### **Question 21**

An e-commerce company wants to block SQL injection and cross-site scripting attacks on its website. Which service should they use?

Select one:

a. AWS WAF

b. AWS Shield

c. AWS Inspector

d. AWS GuardDuty

---

### **Question 22**

Which two AWS services require explicit approval for penetration testing? (Choose 2)

Select one or more:

a. Amazon Route53

b. Amazon RDS

c. AWS Lambda

d. Amazon CloudFront

---

### **Question 23**

A company wants to apply centralized firewall policies across multiple AWS accounts. Which service should they use?

Select one:

a. Amazon GuardDuty

b. AWS Network Firewall

c. AWS WAF

d. AWS Firewall Manager

---

### **Question 24**

Your organization wants to ensure developers follow least privilege principles. Which two IAM features help achieve this? (Choose 2)

Select one or more:

a. Amazon GuardDuty

b. IAM Policies

c. IAM Access Analyzer

d. AWS Shield

---

### **Question 25**

A company wants to test the resilience of their AWS applications by simulating cyberattacks. What is this process called?

Select one:

a. Security Patching

b. Intrusion Prevention

c. GuardDuty Analysis

d. Penetration Testing

# Answers

### **Q1** → d. AWS Shield Standard

*Reason*: Provides automatic DDoS protection by default.

### **Q2** → b. CloudWatch Dashboard

*Reason*: Best for near real-time visualization.

### **Q3** → c & d. Billing metrics + Custom metrics

*Reason*: CloudWatch collects AWS service metrics + custom app metrics.

### **Q4** → c. IAM Policy

*Reason*: Policies only define permissions, don’t make requests.

### **Q5** → d. AWS Trusted Advisor

*Reason*: Gives recommendations across cost, security, performance, and fault tolerance.

### **Q6** → c. Amazon Inspector

*Reason*: Automated security assessment for EC2 & workloads.

### **Q7** → a. Amazon CloudTrail

*Reason*: Logs all API calls in account.

### **Q8** → c. AWS CloudTrail

*Reason*: Identifies who deleted the bucket via API call logs.

### **Q9** → b. AWS GuardDuty

*Reason*: Detects unusual API activity & compromised IAM credentials.

### **Q10** → a & d. ALBs + CloudFront

*Reason*: WAF integrates with ALBs and CloudFront.

---

### **Q11** → b & c. Monitoring API activity + Compliance/auditing

*Reason*: CloudTrail is for logging and compliance.

### **Q12** → c & d. Cost Optimisation + IAM

*Reason*: Trusted Advisor checks cost savings + IAM best practices.

### **Q13** → a. AWS Network Firewall

*Reason*: Provides fine-grained network traffic filtering at VPC level.

### **Q14** → a & b. CloudTrail Events + VPC Flow Logs

*Reason*: GuardDuty analyses logs to detect threats.

### **Q15** → c. CloudWatch Alarms

*Reason*: Can trigger actions when CPU drops below threshold.

### **Q16** → d. Contact AWS Support for authorization

*Reason*: Required before penetration testing.

### **Q17** → c. Shield Advanced provides 24/7 DDoS response team

*Reason*: That’s the key difference.

### **Q18** → a. AWS Firewall Manager

*Reason*: Central service for WAF, Shield, Network Firewall policies.

### **Q19** → b. IAM Roles

*Reason*: Roles provide temporary security credentials.

### **Q20** → c. Amazon Inspector

*Reason*: Scans for software vulnerabilities & missing patches.

### **Q21** → a. AWS WAF

*Reason*: Protects against SQLi and XSS.

### **Q22** → b & d. Amazon RDS + CloudFront

*Reason*: Require explicit AWS approval for pentesting.

### **Q23** → d. AWS Firewall Manager

*Reason*: Enforces firewall policies across accounts.

### **Q24** → b & c. IAM Policies + IAM Access Analyzer

*Reason*: Both enforce least privilege and visibility into permissions.

### **Q25** → d. Penetration Testing

*Reason*: Simulating cyberattacks = pentesting.
