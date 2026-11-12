# Nextech Systems

### ERPNext & Frappe Engineering | Enterprise Integrations | Infrastructure & Automation

**Engineering practical business solutions through open-source technology.**

Nextech Systems is an IT solutions and software engineering practice specializing in ERPNext implementations, custom Frappe development, enterprise integrations, business process automation, and resilient infrastructure.

We bridge the gap between business operations and technology, developing solutions that connect people, hardware, software, and operational data.

Our work focuses on solving real operational challenges, improving business visibility, reducing manual processes, and building systems that businesses can depend on.

## Core Engineering Capabilities

- ERPNext Implementation & Customization
- Frappe Framework Application Development
- REST API Development & Third-Party Integrations
- Android Applications & Mobile Business Workflows
- Jamaican Payroll, Tax & Financial Localization
- Manufacturing & Warehouse Automation
- Biometric Attendance & Workforce Management
- High-Availability Infrastructure & Disaster Recovery
- Linux Systems Administration & Security Hardening
- Database Infrastructure & High Availability
- Virtual IP Management & Automated Failover

---

## Selected Engineering Projects

### 01. Mobile Proof-of-Delivery & Warehouse Logistics

**Industry:** Distribution | Logistics | Warehouse Management

**The Challenge**

Paper-based delivery documentation created operational inefficiencies. Delivery notes could be misplaced, manual scanning consumed administrative time, and delivery confirmation was not consistently available to the back office.

**Architecture**

Developed a custom Android application integrated with ERPNext through a MySQL middleware layer and secured REST APIs.

**Key Features**

- Digital proof-of-delivery and signature capture.
- OCR-assisted delivery note identification and matching.
- QR-provisioned device authentication.
- Automated ERPNext Delivery Trip updates.
- Centralized middleware for mobile transaction processing.

**Business Impact**

- Eliminated lost delivery notes, previously approximately 1 in every 200 deliveries.
- Removed manual scanning and document-upload processes.
- Improved driver accountability through digital signatures.
- Reduced administrative headcount by one.
- Improved delivery visibility and documentation availability.

### 02. Jamaican Statutory Payroll & Tax Engine

**Industry:** Human Resources | Accounting | Payroll

**The Challenge**

Standard payroll configurations required additional localization to support Jamaican statutory calculations, reporting requirements, and financial presentation.

**Architecture**

Developed a customized ERPNext payroll and statutory reporting solution using custom DocTypes, server scripts, and print formats.

**Key Features**

- Progressive PAYE tax band calculations.
- Free-pay threshold handling.
- Annualization rules.
- Automated PAYE rebate calculations around the JMD $6 million threshold.
- TAJ statutory return generation: SO1, SO2 and P24.
- Localized Balance Sheet and Profit & Loss formats.

**Business Impact**

- Automated complex localized payroll calculations.
- Reduced reliance on manual statutory adjustments.
- Standardized payroll reporting outputs.
- Improved consistency between payroll and financial reporting.
- Simplified preparation of statutory return files.

### 03. Multi-Location Biometric Attendance & Overtime Synchronization

**Industry:** Human Resources | Workforce Management

**The Challenge**

Attendance information collected across multiple locations needed to be consolidated into ERPNext. Manual attendance reconciliation and overtime processing created administrative work and inconsistent approval procedures.

**Architecture**

Developed a bidirectional API integration connecting Hikvision biometric attendance terminals with ERPNext.

**Key Features**

- Multi-location Hikvision terminal integration.
- Automated attendance synchronization.
- Lateness and attendance exception tracking.
- Department-head overtime approval workflows.
- Scheduled-shift validation.
- Reversion of unapproved overtime to scheduled shifts.
- ERPNext Timesheet integration.

**Business Impact**

- Centralized attendance information across multiple locations.
- Reduced manual attendance reconciliation.
- Introduced controlled overtime approval procedures.
- Improved workforce reporting consistency.
- Prevented unapproved overtime from automatically becoming payable working time.

### 04. Shop-Floor Manufacturing & Warehouse Picking Kiosks

**Industry:** Manufacturing | Inventory | Production Management

**The Challenge**

Production operators and warehouse personnel needed a more immediate way to record manufacturing activities and inventory movements. Traditional data-entry processes introduced delays between physical operations and ERPNext records.

**Architecture**

Developed real-time, bidirectional kiosk interfaces for machine operators and warehouse picking personnel.

**Key Features**

- Machine-operator production interfaces.
- Job Card execution tracking.
- Machine utilization monitoring.
- Warehouse picking interfaces.
- Pick-list completion tracking.
- Validated stock transaction generation.
- Real-time operational updates.

**Business Impact**

- Reduced delays between physical operations and ERPNext updates.
- Improved visibility into production execution.
- Improved warehouse picking accuracy and traceability.
- Automated validated inventory transactions.
- Reduced reliance on manual data entry.

### 05. High-Availability ERPNext Infrastructure & Disaster Recovery

**Industry:** Enterprise Infrastructure | Business Continuity | Database Engineering

**The Challenge**

Business-critical ERP systems require infrastructure capable of maintaining service availability during individual server failures. Single-server deployments introduce operational risks when hardware, application services, or database services become unavailable.

**Architecture**

Designed and managed a multi-host ERPNext infrastructure incorporating two independent Keepalived instances, each responsible for managing a dedicated Virtual IP (VIP).

The architecture separates frontend application availability from backend database connectivity, allowing each infrastructure layer to maintain its own failover mechanism.

**Key Features**

- Multi-host ERPNext deployment architecture.
- Independent frontend and backend Keepalived instances.
- Dedicated Frontend Application VIP for ERPNext application access.
- Dedicated Backend Database VIP for database connectivity.
- Automated VIP failover between designated application nodes.
- Independent database VIP failover between designated database nodes.
- Separation of application and database network availability management.
- Centralized TrueNAS storage infrastructure.
- Hourly backup snapshots.
- Disaster recovery and restoration planning.

**Business Impact**

- Reduced dependency on individual application servers.
- Established independent failover mechanisms for frontend and backend infrastructure.
- Improved application availability through frontend VIP failover.
- Improved database connectivity resilience through backend VIP failover.
- Centralized backup and recovery infrastructure.
- Established hourly snapshot-based recovery points.
- Improved business continuity and disaster recovery readiness.

---

## Mobile Proof-of-Delivery Architecture

The mobile logistics solution uses a controlled middleware architecture to connect Android devices with ERPNext.

```mermaid
flowchart TD
    A[Driver / Android Device]
    B[QR Device Provisioning]
    C[Secure REST API]
    D[MySQL Middleware Database]
    E[Validation and Processing Layer]
    F[ERPNext]
    G[Delivery Trip Updates]
    H[Digital Proof of Delivery]

    A --> B
    B --> C
    C <--> D
    D <--> E
    E <--> F
    F --> G
    A --> H
    H --> C
```

---

## High-Availability ERPNext Infrastructure

The infrastructure incorporates two independent Keepalived instances, providing separate Virtual IP failover mechanisms for the frontend application layer and backend database layer.

**Frontend Layer:** Keepalived Instance 1 manages the Application VIP, providing a stable access point for ERPNext application hosts.

**Backend Layer:** Keepalived Instance 2 manages the Database VIP, providing a stable database connection endpoint across designated database nodes.

```mermaid
flowchart TB
    U[Users / ERPNext Clients]

    subgraph FRONTEND["Frontend - Application High Availability"]
        direction TB
        K1["Keepalived Instance 1"]
        VIP1["Application VIP"]

        subgraph APP["ERPNext Application Nodes"]
            N1["ERPNext Host A - Active"]
            N2["ERPNext Host B - Standby"]
        end

        K1 --> VIP1
        VIP1 --> N1
        VIP1 -. Failover .-> N2
    end

    subgraph BACKEND["Backend - Database High Availability"]
        direction TB
        K2["Keepalived Instance 2"]
        VIP2["Database VIP"]

        subgraph DB["Database Nodes"]
            DB1["Database Node A - Active"]
            DB2["Database Node B - Standby"]
        end

        K2 --> VIP2
        VIP2 --> DB1
        VIP2 -. Failover .-> DB2
    end

    U --> VIP1
    N1 --> VIP2
    N2 --> VIP2

    subgraph BACKUP["Backup & Disaster Recovery"]
        TN["TrueNAS Centralized Storage"]
        SNAP["Hourly Backup Snapshots"]
        DR["Disaster Recovery"]

        TN --> SNAP
        SNAP --> DR
    end

    DB1 -. Backup .-> TN
    DB2 -. Backup .-> TN
```

**Infrastructure Design Principles**

- Independent frontend and backend failover management.
- Dedicated Virtual IPs for application and database connectivity.
- Separation of application availability from database connectivity.
- Centralized backup storage and recovery planning.
- Reduced reliance on individual server availability.

---

## Technology Stack

| Category | Technologies |
|---|---|
| ERP & Framework | ERPNext, Frappe |
| Programming | Python, Java, JavaScript |
| APIs & Integration | REST APIs, JSON |
| Mobile | Android |
| Databases | MariaDB, MySQL |
| Infrastructure | Linux, Keepalived, TrueNAS |
| High Availability | Virtual IPs, Keepalived Failover |
| Hardware Integration | Hikvision, Biometric Devices |
| Business Systems | Payroll, Accounting, Inventory, Manufacturing |

## Collaboration Opportunities

Nextech Systems welcomes opportunities to collaborate with:

- ERPNext and Frappe implementation partners.
- Software development agencies.
- Businesses requiring specialized ERPNext integrations.
- Organizations seeking infrastructure engineering support.

### Services Available

- ERPNext implementation support.
- Custom Frappe application development.
- Development overflow and subcontracting.
- API and third-party integrations.
- Jamaican statutory payroll and financial localization.
- Mobile and hardware integrations.
- High-availability infrastructure design.
- Linux server administration and infrastructure support.

## Contact Nextech Systems

**Email:** nexxttechja@gmail.com

**GitHub:** https://github.com/nextech-systems/

**Location:** Jamaica

---

*Nextech Systems — Engineering business solutions through open-source technology.*
