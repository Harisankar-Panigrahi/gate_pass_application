# Production Deployment Architecture

## 1. Production Hosting Overview

The Gate Pass Management System is engineered for deployment within enterprise managed hosting environments, dedicated VPS, and standardized Linux/cPanel application servers.

The operational architecture enforces strict directory isolation, ensuring that application business logic, environment secrets, and backend frameworks remain completely inaccessible from the public web document root.

```
+---------------------------------------------------------------------------------+
|                               Production Server                                 |
|                                                                                 |
|   +-------------------------------------------------------------------------+   |
|   |                        Public Web Document Root                         |   |
|   |  - Static Assets (Bundled JavaScript, Stylesheets, Icons, Fonts)        |   |
|   |  - Web Application Entry Point & Single-Page Application Fallback       |   |
|   |  - Web Server Rewriting Directing /api Routes to the Backend Gateway    |   |
|   |  - Progressive Web App Manifest & Service Worker Cache Configuration    |   |
|   +------------------------------------+------------------------------------+   |
|                                        |                                        |
|                                        | Secure Internal Bridge                 |
|                                        v                                        |
|   +-------------------------------------------------------------------------+   |
|   |                   Private Application Core (Non-Public)                 |   |
|   |  - Laravel/PHP Core Backend Engine, Middleware & Domain Services        |   |
|   |  - Environment Configuration (Isolated, Strict Server File Permissions) |   |
|   |  - Application Storage (Encrypted Uploads, Logs, Framework Cache)       |   |
|   |  - Automated Forward-Only Database Migrations                           |   |
|   +------------------------------------+------------------------------------+   |
|                                        |                                        |
|                                        | Protected Database Connection          |
|                                        v                                        |
|   +-------------------------------------------------------------------------+   |
|   |                       Relational Database (MySQL)                       |   |
|   |  - Multi-Tenant Tables, Performance Indexes & Foreign Key Constraints   |   |
|   |  - Least-Privilege Dedicated Database Service Account                   |   |
|   +-------------------------------------------------------------------------+   |
+---------------------------------------------------------------------------------+
```

---

## 2. Environment-Specific Configuration

- **Configuration Isolation:** Distinct configuration files for local development, staging, and production environments prevent accidental environment cross-talk.
- **Secret Separation:** Sensitive cryptographic keys, third-party push notification tokens, and credentials reside strictly in server-level environment variables and are never committed to version control.
- **Restricted Access Permissions:** Server directory permissions restrict read/write access exclusively to the application runtime service account.
- **Secure File Storage:** Storage directories housing visitor photos, employee document attachments, and system logs reside strictly above the public web directory.

---

## 3. Database Migration & Integrity Management

- **Forward-Only Migrations:** Relational database schema adjustments are executed using automated, declarative migration scripts with rollback capability.
- **Performance Indexing:** Strategic database indexes applied to high-traffic columns (`organization_id`, `uuid`, `status`, `expires_at`, `check_in_time`) ensure sub-millisecond query execution under concurrent gate traffic.
- **Integrity Validation:** Relational foreign key constraints and transactional boundaries maintain database consistency across simultaneous visitor and material check-in events.

---

## 4. Web Server Routing & SSL Termination

- **Enforced HTTPS:** Strict Transport Security (HSTS) and mandatory TLS encryption protect all communications between web clients, mobile devices, and the backend API.
- **Security Headers:** Standardized HTTP response headers prevent clickjacking (`X-Frame-Options`), MIME-type confusion (`X-Content-Type-Options`), and cross-origin resource leaks (`Referrer-Policy`).
- **Clean Route Delegation:** Single-Page Application (SPA) routing ensures client-side routes resolve reliably while delegating all `/api` endpoints directly to the backend service engine.

---

## 5. Production Smoke Verification

Following deployment, a standardized verification protocol is executed to confirm system operational readiness:
- Verification of API health endpoints and database connectivity.
- Validation of role-based route protection across administrative and guard portals.
- Testing of mobile client authentication and real-time push notification connectivity.
- Confirmation of active audit logging for all security-sensitive actions.
