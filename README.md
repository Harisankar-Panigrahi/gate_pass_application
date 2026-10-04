# Gate Pass & Visitor Access Management System (STAGS)

An enterprise-grade physical perimeter security, material transit tracking, and digital visitor authorization platform uniting a centralized REST API backend, a high-density web administration portal, and a native Android mobile application.

> **Proprietary Client Project — Portfolio Case Study**  
> *This repository is maintained exclusively for portfolio demonstration, evaluation, and professional reference. The production application source code and infrastructure configuration are proprietary and intentionally excluded.*

---

## Overview

The **Gate Pass & Visitor Access Management System** is a full-stack access control and perimeter management ecosystem designed for commercial office complexes, industrial manufacturing sites, and multi-tenant corporate facilities.

The platform coordinates physical gate operations across multiple stakeholder roles:
- **Security Guards:** Rapid check-in/out, optical QR verification, vehicle logging, and blacklist screening.
- **Facility Managers & Admins:** Multi-tenant organization configuration, gate management, role assignments, and compliance auditing.
- **Host Employees:** One-tap mobile approvals for arriving guests, pre-registration of planned visitors, and digital ID card access.
- **Corporate Visitors & Contractors:** Fast-track registration, digital pass credentials, and seamless entry validation.

---

## Project Highlights

- **Full-Stack Access Control:** Unified web administration portal and native Android mobile application sharing a central REST API.
- **Native Android Client:** Kotlin-based mobile application with CameraX optical QR scanning, offline pass caching, and push notifications.
- **Role-Based Access Control (RBAC):** Tiered authorization enforcing least-privilege access across Super Admins, Facility Admins, Guards, and Employees.
- **Multi-Tenant Organization Isolation:** Strict data segregation across facilities, campus locations, zones, and individual gate lanes.
- **Real-Time Approval Lifecycle:** Instant push notification dispatch enabling host employees to approve or decline visitor arrivals in one tap.
- **Cryptographic QR Verification:** Sub-second, touchless pass verification with tamper-evident nonces and anti-passback protections.
- **Live Facility Occupancy & Muster Roll:** Real-time visibility into all on-site personnel for emergency evacuations and safety audits.
- **Material & Asset Movement Tracking:** Multi-tier authorization workflows for Returnable and Non-Returnable equipment transit with overdue return alerting.
- **Automated Compliance Reporting:** Scheduled generation and delivery of audit-ready PDF and spreadsheet reports.
- **Enterprise Security & Reliability:** Stateless Bearer token authentication, input sanitization, immutable forensic audit trails, and automated test coverage.

---

## Business Problem

In many commercial and industrial facilities, visitor tracking and perimeter security still rely on manual paper logbooks, unverified phone calls, and physical clipboards. These legacy methods introduce severe operational liabilities:

- **Security Blindspots:** Lack of identity verification, no historical records of previous entries, and no automatic screening against security blacklists.
- **Peak-Hour Bottlenecks:** Slow manual handwriting creates long queues at entrance turnstiles and vehicle barriers during shift changes.
- **Disconnected Approvals:** Guards must manually call internal desk phones to verify visitors, causing delays when hosts are away from their desks.
- **Emergency Evacuation Risks:** In the event of a fire or facility emergency, paper logbooks fail to provide an accurate, real-time headcount of who is currently inside the perimeter (Muster Roll).
- **Uncontrolled Asset Movement:** Physical tools, IT equipment, and inventory risk shrinkage or theft without formal, multi-tier transit authorization.

---

## Solution

The platform resolves these vulnerabilities by replacing fragmented paper processes with an automated, synchronized digital workflow:

1. **Digital Visitor Ingestion:** Guests are registered in seconds at guard desks or self-service kiosks with photo capture and government ID references.
2. **Instant Push Approvals:** The backend API immediately dispatches a high-priority push notification to the host employee's Android device, enabling one-tap approval.
3. **Optical Pass Issuance:** Approved visitors receive a time-bound, cryptographically signed QR code displayed on mobile or printed as a visitor badge.
4. **Touchless Verification:** Gate security scans the QR pass using the native Android app or kiosk camera for sub-second entry validation.
5. **Real-Time Accountability:** Live occupancy counters track all personnel inside the perimeter, while immutable audit trails log every entry, exit, and administrative action.

---

## Key Features

- **Visitor Lifecycle Management:** Pre-registration, digital invitations, self-service kiosks, dynamic QR passes, and automated expiration.
- **Digital Employee Badges:** Virtual smart ID cards for company staff with integrated QR credentials, employee ID, and active status indicators.
- **Guard Desk Operations:** High-throughput entry search by pass number, visitor name, vehicle plate, or mobile number, with audited override capabilities.
- **Material Gate Passes:** Returnable vs. Non-Returnable asset movement with sign-offs across Department Heads, Logistics, and Security.
- **Perimeter Security & Lockdown:** One-click emergency lockdown protocol revoking active digital gate passes and initiating real-time headcount reconciliation.
- **Forensic Security Timeline:** Chronological logging of all entry scans, checkout events, and approval decisions with immutable timestamps.
- **Executive Analytics:** Interactive dashboards displaying peak traffic hours, gate utilization rates, and visitor volume trends.

---

## My Role

As the **Full-Stack Lead Engineer**, I architected and implemented the end-to-end Gate Pass Management System:

- **System Architecture & Design:** Defined the multi-tier architecture, domain boundaries, relational database schemas, and RESTful API specifications.
- **Backend API Engineering:** Implemented the core Laravel 11 REST API engine, token-based authentication (Sanctum), multi-tenant organization isolation middleware, and event-driven notification dispatch.
- **Native Android Development:** Engineered the native Android application in Kotlin using Jetpack Compose, CameraX optical scanning, MVVM architecture, and encrypted token storage.
- **Security & Authorization:** Designed the role-based access control (RBAC) engine, multi-step approval state machines, and cryptographic token verification logic.
- **Quality Assurance & Testing:** Developed comprehensive test suites covering unit tests, API contract tests, Android instrumentation, and security edge cases.
- **Production Deployment & Operations:** Configured environment isolation, web server routing, declarative database migrations, and production smoke verification on managed Linux/cPanel infrastructure.
- **State Synchronization & Integration:** Engineered real-time state synchronization between mobile and web clients using Firebase Cloud Messaging and client-side reactive event buses.

---

## Technology Stack

| Category | Technology | Purpose & Implementation |
| :--- | :--- | :--- |
| **Backend** | **Laravel 11 (PHP 8.3+)** | High-performance RESTful API gateway, domain services, business logic |
| **Frontend** | **React & TypeScript (Vite)** | Responsive single-page web dashboard with custom component design system |
| **Mobile** | **Native Android (Kotlin)** | Dedicated client for guards and employees built with Jetpack Compose & MVVM |
| **Mobile Scanning**| **Google CameraX** | Hardware-accelerated optical QR and barcode decoding at gate checkpoints |
| **Database** | **MySQL (InnoDB)** | Normalized relational persistence, multi-tenant scoping, ACID transactions |
| **API Architecture**| **RESTful JSON** | Consistent resource envelopes (`status`, `data`, `meta`, `errors`) |
| **Authentication** | **Laravel Sanctum** | Stateless Bearer token issuance, per-device scoping, and revocation |
| **Notifications** | **Firebase Cloud Messaging**| High-priority real-time push dispatch for visitor approval requests |
| **Hosting & Ops** | **Linux / cPanel / Apache** | Managed production hosting, directory isolation, HTTPS/TLS termination |
| **Testing** | **PHPUnit & AndroidX Test**| Automated unit testing, API contract tests, and mobile ViewModel tests |
| **Development Tools**| **Git & GitHub** | Milestone-driven version management and continuous integration |

---

## System Architecture

```
+---------------------------------------------------------------------------------+
|                               Presentation Layer                                |
|                                                                                 |
|   +------------------------------------+   +--------------------------------+   |
|   |            Web Client              |   |         Android Client         |   |
|   |         (React + TypeScript)       |   |       (Kotlin + Compose)       |   |
|   |  - Administrative Portal           |   |  - Guard Optical QR Scanner    |   |
|   |  - Forensic Security Analytics     |   |  - Host Approval Interface     |   |
|   |  - Material Pass Management        |   |  - Digital ID Cards & Badges   |   |
|   +-----------------+------------------+   +---------------+----------------+   |
+---------------------|--------------------------------------|--------------------+
                      |                                      |
                      | HTTPS / REST (JSON)                  | HTTPS / REST (JSON)
                      | Bearer Token Auth                    | Bearer Token Auth
                      v                                      v
+---------------------------------------------------------------------------------+
|                           API Gateway & Backend Layer                           |
|                                                                                 |
|   +-------------------------------------------------------------------------+   |
|   |                        Laravel 11 RESTful Engine                        |   |
|   |                                                                         |   |
|   |  - Token Authentication & Session Management (Sanctum)                  |   |
|   |  - Multi-Tenant Organization Isolation Middleware                       |   |
|   |  - Role-Based Access Control Policies (RBAC)                            |   |
|   |  - Cryptographic Pass Token Generator & QR Verification Engine          |   |
|   |  - Firebase Cloud Messaging (FCM) Push Notification Dispatcher          |   |
|   |  - Event-Driven Audit & Forensic Timeline Logger                        |   |
|   +------------------------------------+------------------------------------+   |
+----------------------------------------|----------------------------------------+
                                         |
                                         | PDO / Eloquent ORM
                                         v
+---------------------------------------------------------------------------------+
|                               Persistence Layer                                 |
|                                                                                 |
|   +-------------------------------------------------------------------------+   |
|   |                      Relational Database (MySQL)                        |   |
|   |  - Organizations, Locations, Gates & Turnstiles                         |   |
|   |  - Users, Roles, Permissions & Active Device Tokens                     |   |
|   |  - Visitors, Hosts, Gate Passes & Digital Badges                        |   |
|   |  - Material Movement Records & Asset Return Tracking                    |   |
|   |  - Immutable Access Logs & Security Incident Audits                     |   |
|   +-------------------------------------------------------------------------+   |
+---------------------------------------------------------------------------------+
```

---

## Application Modules

The system is organized into 18 specialized modules ensuring separation of concerns:

1. **Authentication:** Multi-role login, token issuance, per-device revocation, and role-based policies.
2. **Executive & Operational Dashboards:** Real-time occupancy counters, capacity gauges, and pending approval queues.
3. **Visitor Management:** Visitor directory, identity photo capture, document attachments, and visit history.
4. **Visitor Approvals:** Real-time push notification approvals, one-tap accept/decline, and automatic timeout routing.
5. **Gate Pass Lifecycle Management:** Pass state machines (`Pending`, `Approved`, `ActiveInside`, `CheckedOut`, `Expired`, `Revoked`).
6. **QR Verification Engine:** Optical cryptographic token verification, anti-passback enforcement, and expiration checks.
7. **Gate Operations & Kiosks:** High-throughput guard desk interface supporting multi-parameter search and audited overrides.
8. **Registered Persons & Contractors:** Long-term site contractor lifecycle, digital badge provisioning, and status management.
9. **Access Rules & Policy Engine:** Granular zone, building, and time-of-day access restrictions by personnel classification.
10. **Material Gate Passes:** Returnable/non-returnable asset movement with multi-tier approvals and overdue return tracking.
11. **Notification Infrastructure:** High-priority push notifications via FCM, transactional credential emails, and alert centers.
12. **Security Operations & Forensics:** Watchlist screening, automated security alert triggers, and chronological forensic audits.
13. **Executive Analytics:** Traffic volume heatmaps, peak entry hour analysis, and gate throughput metrics.
14. **Automated Reports:** Scheduled daily/weekly/monthly audit reports exportable to PDF and spreadsheet formats.
15. **Emergency Management:** One-click perimeter lockdown and live Muster Roll Call evacuation reconciliation.
16. **Android Application:** Purpose-built native Kotlin client for mobile guard scanning and host approvals.
17. **Profile & Security Settings:** Self-service credential updates, organization security policies, and active session inspection.
18. **Production Operations:** Environment isolation, automated database migrations, and operational monitoring.

---

## Native Android Application

The mobile component is a native Android application engineered in **Kotlin** adhering to **Clean Architecture** and **MVVM**:

- **Modern Declarative UI:** Built with **Jetpack Compose** utilizing Material 3 design tokens, responsive layouts, and system dark/light adaptation.
- **Hardware-Accelerated Optical Scanning:** Embedded **CameraX** pipeline with real-time barcode analysis capable of sub-second pass verification under challenging lighting conditions.
- **Encrypted Local Storage:** Authentication tokens and sensitive state are persisted via **EncryptedSharedPreferences** backed by the Android Keystore.
- **Real-Time Host Approvals:** Full FCM integration enabling host employees to receive push notifications and approve or reject visitor arrivals directly from their mobile devices.
- **Offline Resilience:** Active passes and visitor verification statuses are cached locally, allowing guards to verify credentials during transient network disconnects.
- **State Synchronization:** Background event buses and Kotlin Flows dynamically refresh badge counts and pass lists without requiring manual app reloads.

*(Note: The Android application source code, keystore files, and APK binaries are proprietary and intentionally excluded from this portfolio repository).*

---

## Testing & Quality Assurance

Quality assurance was integrated across all development phases:

- **Unit Testing:** Validates business domain models, status transitions, token utilities, and helper functions.
- **API Contract Testing:** Automated verification of REST API endpoints validating expected JSON envelopes, HTTP status codes, and validation rules.
- **Integration Testing:** Confirms multi-tenant data segregation, workflow state sequences, and material pass lifecycles.
- **Android Instrumentation Testing:** Tests CameraX scanner stability, UI state composables, and encrypted storage operations.
- **Authentication & Authorization Testing:** Verifies token lifecycles, session timeouts, and role-based policy enforcement.
- **State Synchronization Testing:** Tests real-time notification delivery and UI reactivity under concurrent check-in conditions.
- **Regression & Production Verification:** Pre-flight smoke tests validating API latencies, migration integrity, and SSL encryption.

---

## Production Deployment

The system is engineered for enterprise managed hosting environments (Linux, cPanel, Dedicated VPS):

- **Directory Isolation:** The private application core, `.env` configurations, and uploaded visitor documents reside strictly above the public document root (`public_html`), preventing web traversal.
- **Environment Separation:** Development, staging, and production environments maintain isolated configurations with locked server environment variables.
- **Forward-Only Migrations:** Relational database schemas are updated via declarative migrations with indexed query optimization.
- **Enforced Encryption:** Mandatory HTTPS/TLS termination and standardized security headers (`HSTS`, `X-Frame-Options`, `X-Content-Type-Options`).

---

## Security Architecture

- **Stateless Bearer Authentication:** Secure API token management with per-device scoping and instant revocation.
- **Role-Based Access Control:** Least-privilege policies enforced at the route, controller, and database query levels.
- **Anti-Passback & Cryptographic Validation:** Optical passes embed unique cryptographic nonces preventing replay or duplicate pass sharing.
- **Audit Trail Immutability:** Every critical administrative action, security override, and check-in event creates an immutable audit log.
- **Sanitized Inputs:** Strict server-side validation and prepared statements mitigating SQL injection and XSS vulnerabilities.

---

## Project Status

The Gate Pass Management System is a **production-oriented, proprietary client application**. 

This repository is maintained as a technical portfolio case study showcasing system design, architecture, and engineering implementation. Access to the proprietary source code, production deployment, and client infrastructure is restricted.

---

## Portfolio Notice

> **This repository is a portfolio and technical case-study representation of a proprietary production application.**  
>   
> **The actual production source code, infrastructure configuration, credentials, database, deployment scripts, and other proprietary implementation materials are intentionally excluded.**  
>   
> **Access to the complete application or source code is available only with appropriate authorization.**

---

## Technical Documentation

Explore the detailed architectural and engineering documentation in the [`docs/`](docs/) directory:

- [System Architecture Specification](docs/architecture.md)
- [Enterprise Feature Catalog](docs/features.md)
- [Core Application Modules Breakdown](docs/modules.md)
- [Development Process & Engineering Methodology](docs/development-process.md)
- [Testing Strategy & Quality Assurance](docs/testing.md)
- [Production Deployment Architecture](docs/deployment-overview.md)
- [Portfolio & Case-Study Notice](PORTFOLIO_NOTICE.md)
- [Security Policy](SECURITY.md)

---

## Contact

This project is maintained as a technical portfolio piece by **Harisankar Panigrahi**.

- **Specialization:** Full-Stack Web Development, Enterprise Laravel API Architecture, Native Android (Kotlin/Compose), System Design
- **Available for:** Freelance Contracts, Full-Time Engineering Roles, System Architecture Consulting
- **Email:** `p.harisankar03@gmail.com`
- **LinkedIn:** [Harisankar Panigrahi](https://www.linkedin.com/in/harisankar-panigrahi/)
- **Freelance Inquiries:** Available via Upwork / Fiverr / Direct Contract
