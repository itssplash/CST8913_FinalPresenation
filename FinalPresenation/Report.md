
# CST8913 - Migration Presentation

## Develop a Migration Strategy

### Assessment

#### Identify Resources:
- **150 VM’s**: Running Windows or Linux server.
- **Monolithic ERP System**: Part of the SQL Database, used for financial and inventory management.
- **SQL Database Cluster**: 10 databases for customer and operational data.
- **E-Commerce Applications**: Strict uptime requirements.
- **Legacy Mainframe System**: 10 mainframes used for payroll and reporting.

#### Migration Priorities:
- **Mainframe**: Prioritize load balancing, networking, computational processing; add regions/zones to avoid orphaned data.
- **SQL Database**: Prioritize VNet networking and grouping; add regions/zones.
- **VMs**: Ensure scalability, availability, and regional zone distribution.

#### Define Scope:
- **Regions**: US and Canada (primary location: Ottawa, Canada).
- **Zones**: Canada Central, Canada East, East US, East US 2.
- Separate VMs and Databases equally among zones and regions.

---

### Migration Tools:
- **Azure Migrate**: Assess and migrate VMs.
- **Azure Cost Calculator**: Estimate migration costs.
- **Azure Migrate Appliance**: On-premises discovery.
- **Azure Compliance**: Ensure regulatory adherence.
- **Web App Migration Assistant**: Migrate e-commerce apps.
- **Azure Database Migration Service**: Migrate SQL databases.

---

### Azure Resources Used for Migration
- **VMs**: Azure Virtual Machines (IaaS).
- **Database**: Azure SQL Database (PaaS).
- **ERP**: Azure App Service (PaaS) or Azure Kubernetes Service (AKS) for refactoring.
- **Mainframe**: Azure Logic Apps or Azure Functions for workflows/modernization.
- **E-commerce Apps**: Azure App Service or AKS.

---

### Migration Approach in Phases:
1. **Phase 1**: Non-critical systems (low-risk migration).
2. **Phase 2**: SQL databases and internal VMs.
3. **Phase 3**: Critical applications (ERP and e-commerce).
4. **Phase 4**: Legacy mainframe modernization.

---

## Migration Workflow (Workflow Architecture on Azure)

### 1. Application VMs (Rehosting: IaaS)
**Workflow**:
- Use **Azure Migrate** to assess and migrate 150 on-prem VMs to **Azure Virtual Machines**.
- Group workloads in **Resource Groups**, configure **Availability Sets/VM Scale Sets**, and enable disaster recovery with **Azure Site Recovery (ASR)**.

**Architecture Type**:
- **IaaS**: Maintains full control and replicates the current environment for compatibility with legacy systems.

---

### 2. Monolithic ERP (Refactoring: PaaS)
**Workflow**:
- Break the ERP monolith into microservices.
- Containerize with **Docker** and orchestrate with **Azure Kubernetes Service (AKS)**.
- Host APIs and front-end on **Azure App Service**.
- Migrate ERP data to **Azure SQL Database (Managed Instance)**.

**Architecture Type**:
- **PaaS**: Simplifies infrastructure management and provides scalability for ERP workloads.

---

### 3. Legacy Mainframe (Modernizing: SaaS)
**Workflow**:
- Replace workflows (e.g., payroll) with **Azure Logic Apps** and **Azure Functions** for serverless automation.
- Use **Azure API Management** for secure integrations.

**Architecture Type**:
- **SaaS**: Reduces overhead by leveraging managed services for workflow automation.

---

### 4. SQL Database Cluster (Modernizing: PaaS)
**Workflow**:
- Use **Azure Database Migration Service** to migrate to **Azure SQL Database (Managed Instance)** or **Hyperscale**.
- Ensure data synchronization with **Azure SQL Data Sync**.

**Architecture Type**:
- **PaaS**: Streamlines database management with built-in scalability and compliance features.

---

### 5. E-commerce Applications (Modernizing: PaaS)
**Workflow**:
- Assess and migrate apps to **Azure App Service** with **Azure App Service Migration Assistant**.
- Optimize traffic using **Azure Front Door** and secure routing with **Azure Application Gateway**.
- Enhance performance with **Azure Redis Cache**.

**Architecture Type**:
- **PaaS**: Offloads infrastructure management and ensures scalability for public-facing applications.

---

### 6. Data Migration and Security
**Workflow**:
- Migrate SQL and file data using **Azure Database Migration Service** and **Azure Storage Migration Tool**.
- Encrypt all data with **Azure Key Vault**.
- Use **Azure Backup** for disaster recovery and **Azure Policy** for GDPR/HIPAA compliance.

**Architecture Type**:
- **PaaS/Storage Services**: Ensures cost-effective, secure, and scalable storage for structured and unstructured data.

## High level diagram 

![Blank diagram (11)](https://github.com/user-attachments/assets/1c96cc07-6b52-483d-86bf-538ae4a6f803)


## Execution

The execution step involves actual implementation of the planned migration activity using various services and tools provided by Azure, which will enable smooth transition with minimum possible downtime. The details of the execution are as follows:

### Rehosting Virtual Machines (VMs):
- Use Azure Migrate to assess and rehost 150 on-premises VMs to Azure Virtual Machines.
- Availability Sets or VM Scale Sets configuration should be set up for High Availability.
- Azure Site Recovery implementation to provide disaster recovery and fault tolerance for the application.

### Refactor ERP System:
- The monolithic ERP system shall be broken down into microservices to support better scalability.
- Containerize the services using Docker and deploy them on Azure Kubernetes Service-AKS.
- Migrate the ERP data to Azure SQL Database Managed Instance, which will ensure compatibility with existing applications.

### Modernization of Legacy Mainframes:
- Workload lift and shift to Azure Virtual Machines to maintain compatibility.
- Use Azure Logic Apps and Azure Functions to modernize workflows.
- Secure integrations are implemented using Azure API Management.

### Database Migration:
- Perform migrations to Azure SQL Database Hyperscale using the Azure Database Migration Service.
- Use Azure SQL Data Sync to keep data in sync and reduce downtime during cutover.

### E-commerce Applications:
- Modernize e-commerce applications to Azure App Service using the Web App Migration Assistant.
- Optimize traffic flow using Azure Front Door, and route securely with Azure Application Gateway.
- Use Azure Redis Cache to improve performance in high-demand scenarios.

### Data Migration:
- Structured and unstructured data are migrated using the Azure Storage Migration Tool.
- Encrypt data with Azure Key Vault and configure automated backups with Azure Backup for disaster recovery.

---

## Validation

The most important part of validation is ensuring that the resources will function correctly after migration, the data integrity is preserved, and the performance baselines are met.

### Functional Validation:
- Application functionality should be tested by running predefined test scenarios on the applications, such as ERP.
- Ensure the integrity of database operations, including stored procedures, triggers, and data consistency.

### Performance Testing:
- Test the scalability of Azure Virtual Machines and AKS clusters with Azure Load Testing.
- Measure query execution times and overall database performance to meet or exceed on-premises benchmarks.

### Compliance Validation:
- Verify that GDPR, HIPAA, and CCCS standards are met using Azure Policy.
- Run a security audit using Azure Security Center to make sure all configurations meet industry standards.

### Disaster Recovery Validation:
- Test RPO/RTOs by running failover scenarios using Azure Site Recovery.
- Validate backup and restoration processes using Azure Backup.

### User Acceptance Testing (UAT):
- Engage the end users to validate that the ERP system and e-commerce applications are usable.
- Incorporate user feedback to fix post-migration issues.

---

## Post-Migration Optimization:
- Perform fine-tuning of resource configuration settings based on performance test results.
- Decommission the legacy systems and retire unused resources to optimize costs.

---

## Address Legacy System Modernization

The modernization of legacy systems will use a combination of refactoring and rehosting approaches. The monolithic ERP system will be broken into smaller microservices to improve scalability and performance. These microservices will be hosted on Azure Kubernetes Service (AKS), while legacy components will be replaced with modern solutions like APIs managed through Azure API Management and serverless functions on Azure Functions. This approach reduces complexity and allows the ERP system to adapt to future needs.

For the legacy mainframe system, a lift-and-shift approach will migrate workloads to Azure Virtual Machines (VMs) using Azure Migrate. This ensures minimal changes while keeping operations uninterrupted. Network optimization will be achieved using Azure Virtual Network (VNet) and Azure ExpressRoute for secure, fast connectivity. Over time, mainframe workflows will be modernized with Azure Logic Apps and Azure Functions, providing efficient automation. This strategy combines IaaS for legacy systems and PaaS for scalable solutions, ensuring compliance, reducing downtime, and improving overall performance.

---

## Ensure Compliance and Security

There are three fundamental areas of security to highlight to ensure that the migration is both compliant and secure: Backups/Disaster recovery, Encryption, Antivirus/Malware Software, Authorization/Compliance and most importantly, Networking.

### Legacy VMs (Rehosting: IaaS)
For legacy VM’s rehosting to IaaS, you must consider the compliance and security measures of the Azure VM equivalent.

#### Backup/Disaster Recovery:
- For VMs that are suffering from disasters such as regional outages, environmental disasters, and irreparable vulnerabilities, Disaster recovery is a security measure to consider.
- For the company migration, apply Azure Site Recovery for VM replication failover.
- For Azure Site Recovery, you must identify the source VM to replicate and the target resources that define the replicate.
- For the target region, Canada East, US East, and US East2 are good choices.
- Azure Site Recovery will automatically create the target resources for the target region such as storage, networks, and zones.
- Lastly, set the replication policy, which states VM recovery point snapshot times.
- For consistent availability and failover, use the default recovery point retention of once per day and turn app-consistent snapshot frequency off.
- The reason behind this is that Azure app-consistent snapshots on the hour may take a snapshot of corrupted data if the snapshot occurs whilst transactions are in progress. It is preferable to set up app-snapshots to occur after an action is completed such as after a transaction.

#### Encryption:
- Encryption for VMs can be applied to the disks and uses Azure Key Vault to store the encryption keys and secrets.
- In the case of server VMs, it can provide a measure of authentication by having specific roles such as administrators accessing certain decryption keys to VMs OS disk within Azure Key Vault.
- Encryption can also be applied to the networking level to encrypt data in transit.

#### Network:
Networking is an important aspect of VM security as a VM must be able to connect to the public in a secure manner. A good mindset to secure networking is to privatize networks if possible. Azure supplies multiple services for secure VMs:
- **Configure Network Access Control**: Limit VM connectivity to specified areas such as buildings.
- **Azure Firewall**: Provides filtering of traffic and malware by blocking IP addresses (Layer 3) and analyzing vulnerable packets (Layer 7).
- **Global Load Balancing**: Azure Traffic Manager as a DNS load balancer and VM connectivity by using VPNs.

#### Authorization/Compliance:
- Configure IAM Roles and permissions for VM management (Administrator should have subscription management and read/write access. Developers should have read/write access and employee read access).
- Azure VMs and services follow many compliance offerings to the cloud. For the migration of an e-commerce business, it is important to note if the primary region is Canada, to confirm compliance to Canadian laws and policies.
- Azure has compliance offerings of Canadian Center for Cybersecurity (CCCS) for protected B assets such as an individual’s payment information.

#### Anti-virus/Anti-Malware:
- Azure offers **Microsoft Defender for VMs** as anti-malware software.
- Using Microsoft Defender protects VMs by analyzing for malware or viruses and removing them from the affected system. It is yet another layer of security to protect the VMs.

---

## 2. Monolithic ERP, E-Commerce, and Database Cluster (Refactoring: PaaS)

#### Authorization:
- Use Azure Kubernetes Service’s (AKS) Role-based access controls to set roles for services on a team management basis (such as the accounting team should only have access to accounting services) and require authorization for container registries.

#### Networking:
- Ensure privatization of networking, use private internal IP addresses and Azure Site-to-Site VPN or Express Route.
- Configure networking ports. Ensure that AKS pods are not accessing or using vulnerable ports within the architecture.

#### Encryption:
- Use Kubernetes secrets to store company passwords and certificates involving services made with Kubernetes pods.

#### Backup/Disaster Recovery:
- Ensure automation of pod replacement using AKS and self-healing for repair down-times.
- AKS should automatically fail over to another cluster if there is a regional outage or failure.
- Ensure Kubernetes clusters are split into different regions for disaster recovery and high availability, and split pods into different zones.
- Ensure each region contains 2 or 3 Master nodes, one for each cluster. 2 clusters per region.

---

## 3. Legacy Mainframe (Modernizing: SaaS)

#### Anti-virus/Anti-Malware:
- Azure Functions also use Microsoft Defender as a security measure against malware and viruses.
- Microsoft Sentinel can also be used as a monitoring or logging system to log affected systems.

#### Networking:
- Secure Azure Functions HTTP endpoints by using HTTPS, requiring access keys, using app service authorization, using VNet connections, and ensuring isolation of functions.
- Another networking security measure is to make sure admin endpoints are disabled to prevent unintentional admin access.

#### Authorization/Compliance:
- Azure Functions use API management to require specific requests to be authenticated.
- Certain roles such as developer may require authentication to use software such as requesting GraphQL.
- Identities can be assigned using Microsoft Entra ID to the application to manage user access of numerous services.
- For compliance, AKS shares the same compliance policies with VMs.

#### Encryption:
- By default, Azure encrypts storage account data when it is at rest using customer-managed keys and shared access tokens (SaS).





## References

### Mainframes
- [IBM: What is a Mainframe?](https://www.ibm.com/topics/mainframe#:~:text=A%20centralized%20computing%20environment%20has,servers%20(or%20data%20servers).)

### Assessment
- [Azure Cloud Adoption Framework: Assess](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/migrate/assess/)

### Migration Plan
- [2toLead: What is a Migration Plan and How to Prepare](https://www.2tolead.com/insights/what-is-a-migration-plan-and-how-to-prepare)

### Security
- [Azure AKS Security Concepts](https://learn.microsoft.com/en-us/azure/aks/concepts-security)
- [Azure Functions Security Concepts](https://learn.microsoft.com/en-us/azure/azure-functions/security-concepts)
- [Virtual Machine Security Fundamentals](https://learn.microsoft.com/en-us/azure/security/fundamentals/virtual-machines-overview)

### Replication
- [Azure Site Recovery Architecture](https://learn.microsoft.com/en-us/azure/site-recovery/azure-to-azure-architecture)
- [Azure Site Recovery FAQ](https://learn.microsoft.com/en-us/azure/site-recovery/azure-to-azure-common-questions)

### Compliance
- [Azure Compliance Overview](https://learn.microsoft.com/en-us/azure/compliance/)
- [CCCS Compliance: Regulatory Offering](https://learn.microsoft.com/en-us/compliance/regulatory/offering-cccs-medium)

### Encryption
- [Azure Disk Encryption Overview](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/disk-encryption-overview)

### Networking
- [Azure Networking Security Overview](https://learn.microsoft.com/en-us/azure/security/fundamentals/network-overview)

### Legacy Modernization
- [Modernizing Legacy Applications](https://www.oreilly.com/library/view/modernizing-legacy-applications/9781804616659/)
