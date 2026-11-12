# Awesome-Role-Based-Access-Control-Multi-Admin-Approval

# Awesome Role-Based Access Control & Multi-Admin Approval

> A curated list of top Role-Based Access Control (RBAC) and Multi-Admin Approval platforms — both SaaS/Hosted commercial solutions and open-source alternatives for enforcing least-privilege access, separation of duties, and governed approval workflows.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Okta](#okta)
  - [Microsoft Entra ID](#microsoft-entra-id)
  - [CyberArk Identity](#cyberark-identity)
  - [JumpCloud](#jumpcloud)
  - [OneLogin](#onelogin)
  - [PingOne](#pingone)
  - [Auth0](#auth0)
  - [Druva](#druva)
- [Open-Source Software](#-open-source-software)
  - [KubeVirt Shepherd](#kubevirt-shepherd)
  - [Keycloak](#keycloak)
  - [Casbin](#casbin)
  - [Ory Keto](#ory-keto)
  - [Permit](#permit)
  - [OpenFGA](#openfga)
  - [SpiceDB](#spicedb)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted RBAC and Multi-Admin Approval platforms. These are not open-source but are included as reference points for feature comparison.

### Okta
**Type:** Enterprise IAM with standard and custom admin roles
Okta provides standard admin roles (Super Admin, Org Admin, App Admin, Group Admin, Read-Only Admin, etc.) with predefined permissions, plus custom roles that bundle granular permissions like `okta.apps.manage` and `okta.users.appAssignment.manage` [citation:2][citation:14]. Role assignments can be scoped to specific resources (e.g., a particular app or group) for least-privilege access. IAM-based standard roles (Access Certifications Admin, Access Requests Admin, Workflows Admin) are immutable but bundle preset permissions. **Best for:** Organizations needing mature, well-documented RBAC with resource-scoped role assignments and cross-resource permission composition.

### Microsoft Entra ID
**Type:** Identity platform with built-in and custom roles
Entra ID provides built-in roles (Global Admin, User Admin, App Admin) and custom roles that can be assigned at Tenant, Administrative Unit, or specific resource scope (groups, enterprise apps, app registrations) [citation:3]. Role assignments can target users, role-assignable groups, or service principals. PIM (Privileged Identity Management) enables just-in-time role activation with approval workflows and audit trails. **Best for:** Microsoft-centric organizations needing scope-constrained role assignments and PIM-based approval for privileged roles.

### CyberArk Identity
**Type:** Identity administration with role-based rights and approval
CyberArk Identity uses roles as the unit of access control, assigning application access, administrative rights, and policies to roles rather than individual users [citation:4]. The System Administrator role is immutable and contains all privileges; custom roles can be created with specific administrative rights (e.g., manage users, create roles, run reports). Roles can be created with members, permissions, and applications assigned in any order. **Best for:** Organizations needing a centralized identity platform where roles bundle both app access and administrative privileges.

### JumpCloud
**Type:** Cloud directory with custom admin roles
JumpCloud supports custom admin roles built from permission categories including Access Management, Application Management, Core Administration, Device Management, and Role Management [citation:7]. Each category has granular sub-permissions (Full Access, View, No Access, or Create/Update/Delete). A maximum of 20 custom roles is supported. Only Admins with Billing (Super Admin equivalent) can create and edit custom roles. **Best for:** SMBs and mid-market organizations wanting granular custom admin roles within a cloud directory.

### OneLogin
**Type:** IAM with role-based app access and mappings
OneLogin roles are collections of apps; assigning a user to a role grants access to all apps in that role . Mappings can automatically assign users to roles based on directory attributes (e.g., Department = HR). Role admins can be scoped to specific roles, and manual vs. mapping-based role assignments must be managed consistently. **Best for:** Organizations wanting app-centric role management with attribute-based automatic assignment.

### PingOne
**Type:** Identity platform with built-in and custom admin roles
PingOne provides built-in admin roles (Organization Admin, Environment Admin, Identity Data Admin, etc.) with defined role-assignment hierarchies [citation:6]. For example, Environment Admin can assign all roles except Organization Admin. Custom roles can be created with granular permission identifiers. Role assignments can be automatic, group-based, or user-based. **Best for:** Organizations needing hierarchical admin role structures with constrained delegation.

### Auth0
**Type:** Developer IAM with dashboard roles
Auth0 provides dashboard roles including Admin (full read/write), Editor roles for Connections, Key Management, Organizations, Specific Apps, and Users, plus Viewer roles for read-only access [citation:10]. Roles can be scoped to specific applications (Editor - Specific Apps) for least-privilege access. Support Access roles control ticket management. **Best for:** Developer teams wanting granular dashboard access control without full admin privileges.

### Druva
**Type:** Data protection with custom admin roles and view-only RBAC
Druva provides customizable admin roles built from rights including Backup Configuration, Restore Management, Server Management, Reporting, Policy Management, and Disaster Recovery [citation:1]. A **Druva Cloud Platform View-Only Administrator** role was introduced specifically for Cyber Resiliency features, allowing SecOps teams to view ransomware detection, threat hunting, and audit trails without the high-privilege Cloud Admin role [citation:13]. View-only admins cannot create, edit, or delete—UI elements and APIs are blocked accordingly. **Best for:** Druva customers needing separation of duties between backup admins and security operations teams.

---

## 🟩 Open-Source Software

Self-hosted, community-driven RBAC and approval workflow tools. The open-source ecosystem spans **governance-first platforms with built-in approval**, **authorization engines**, and **relationship-based access control systems**.

### KubeVirt Shepherd
**Stack:** Go / React / PostgreSQL / Kubernetes | **License:** Open Source (Alpha)
Shepherd is a governance-first management platform for KubeVirt VMs with **built-in approval workflows** for create, modify, start, stop, restart, and delete operations [citation:12]. It combines platform RBAC with System, Service, and VM membership inheritance, environment-scoped global role bindings, and a full audit trail for governed resource changes. Designed as a vendor-neutral alternative to OpenShift Virt, it validates the core governance path (approval workflows, RBAC, audit trails) in a financial-services environment. PostgreSQL-only runtime with River Queue for async work. **Alpha status**—core paths validated but broader external feedback is pending. **Best for:** Kubernetes/KubeVirt teams needing self-service VM provisioning with structured multi-admin approval and audit trails.

### Keycloak
**Stack:** Java | **License:** Apache-2.0
Keycloak is the most widely deployed open-source IAM platform, providing realm-level roles, client roles, composite roles, and group-based role mapping. Fine-grained authorization services allow defining resources, scopes, and policies (role, user, client, time, aggregate) for complex access decisions. Admin console access is controlled via admin roles. **Trade-off:** Approval workflows are not built-in for admin actions—you build them on top using custom extensions or external orchestration.
**Best for:** Organizations wanting a proven IAM foundation with rich role modeling and policy-based authorization, accepting that multi-admin approval for role changes must be implemented separately.

### Casbin
**Stack:** Go / Multi-language | **License:** Apache-2.0
Casbin is an authorization library supporting ACL, RBAC, ABAC, and RESTful access control models across multiple languages (Go, Java, Node.js, Python, etc.). Models and policies are defined in configuration files, allowing flexible role inheritance and custom access logic. **Trade-off:** It is a library, not a platform—you embed it in your application and build admin UI, approval, and audit on top.
**Best for:** Developers wanting a flexible, embeddable authorization engine with model-driven RBAC/ABAC policies.

### Ory Keto
**Stack:** Go | **License:** Apache-2.0
Ory Keto is an open-source authorization server implementing Google Zanzibar-style relationship-based access control (ReBAC). It answers "can subject X do action Y on object Z" using relationship tuples, supporting fine-grained permissions that can model RBAC, ABAC, and hierarchical access. **Trade-off:** No built-in approval workflow—Keto handles authorization decisions, not multi-admin approval processes.
**Best for:** Teams wanting scalable, fine-grained authorization with relationship-based models, pairing it with a separate approval layer.

### Permit
**Stack:** (Check repository) | **License:** Open Source (core)
Permit is an open-source authorization framework with a policy-as-code approach, supporting RBAC, ABAC, and ReBAC. It provides a UI for managing roles and permissions, SDKs, and a decision engine. **Trade-off:** The open-source core may lack advanced enterprise features like approval workflows; verify current feature set.
**Best for:** Teams wanting a developer-friendly authorization layer with policy-as-code and a management UI.

### OpenFGA
**Stack:** Go | **License:** Apache-2.0
OpenFGA is a CNCF project implementing fine-grained authorization inspired by Google Zanzibar, with a DSL for defining authorization models and APIs for checking permissions. It supports relationship-based access control and can model RBAC, ABAC, and contextual tuples. **Trade-off:** Like Keto, it is an authorization engine—approval workflows must be built separately.
**Best for:** Organizations wanting a CNCF-backed, Zanzibar-style authorization system with strong community support.

### SpiceDB
**Stack:** Go | **License:** Apache-2.0
SpiceDB is a Zanzibar-inspired database for permissions, designed for low-latency authorization checks at scale. It supports schema-based permission definitions and relationship tuples. **Trade-off:** Authorization engine only—no approval workflow or admin UI out of the box.
**Best for:** Teams needing high-performance, scalable authorization checks with a proven Zanzibar model.

---

## 📊 Comparison at a Glance

| Software | License | Stack | Built-in Approval | RBAC Model | Self-Hosted | Best For |
|----------|---------|-------|-------------------|------------|-------------|----------|
| **Okta** | Proprietary | Cloud | (Via workflows) | ✅ Standard + custom | ❌ | Enterprise IAM + scoped roles |
| **Microsoft Entra ID** | Proprietary | Cloud | ✅ PIM | ✅ Built-in + custom | ❌ | Microsoft ecosystem + PIM |
| **CyberArk Identity** | Proprietary | Cloud | (Check) | ✅ Role-based rights | ❌ | Identity admin + app access |
| **JumpCloud** | Proprietary | Cloud | ❌ | ✅ Custom admin roles | ❌ | SMB cloud directory |
| **OneLogin** | Proprietary | Cloud | ❌ | ✅ App-centric roles | ❌ | Attribute-based role mapping |
| **Druva** | Proprietary | Cloud | (View-only role) | ✅ Custom admin rights | ❌ | Data protection separation of duties |
| **KubeVirt Shepherd** | Open Source | Go/Postgres | ✅ Built-in | ✅ Platform + membership | ✅ | KubeVirt VM governance + approval |
| **Keycloak** | Apache-2.0 | Java | ❌ | ✅ Realm/client/composite | ✅ | Proven IAM foundation |
| **Casbin** | Apache-2.0 | Multi-language | ❌ | ✅ Model-driven | ✅ (Library) | Embeddable authorization |
| **Ory Keto** | Apache-2.0 | Go | ❌ | ✅ ReBAC (Zanzibar) | ✅ | Fine-grained relationship authz |
| **OpenFGA** | Apache-2.0 | Go | ❌ | ✅ ReBAC (Zanzibar) | ✅ | CNCF-backed authorization |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source RBAC or Multi-Admin Approval tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem **splits sharply** between **authorization engines** (Keycloak, Casbin, Ory Keto, OpenFGA, SpiceDB) that answer "can X do Y on Z" but do **not** include multi-admin approval workflows, and **governance platforms with built-in approval** (KubeVirt Shepherd) that combine RBAC, approval, and audit for specific resource types. For **multi-admin approval** specifically, open-source options are extremely limited—Shepherd is the only project found with native approval workflows baked into its governance model [citation:12]. Commercial platforms like Okta, Entra ID (via PIM), and Druva offer approval-adjacent capabilities (workflows, JIT activation, view-only roles) but are not fully open-source.

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
