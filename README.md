<h1 align="center">🔐 Enterprise Identity Lifecycle Automation: Joiner-Mover-Leaver Pipeline in Microsoft Entra ID</h1>

<h3 align="center">
Built by <span style="color:#0078D4;">Divine Oguamanam</span>
</h3>

---

<h2>📌 Project Overview</h2>

Modern organizations manage employee identities across multiple departments, offices, and business units. When identity management is handled manually, companies face major security and operational problems such as:

- Delayed onboarding
- Incorrect access assignments
- Excessive permissions
- Forgotten user accounts
- Slow employee offboarding
- Lack of governance visibility

This project demonstrates a complete enterprise Identity Lifecycle Management deployment using Microsoft Entra ID inside a simulated company environment called <b>AeroMedia Global</b>.

The implementation focused on building a secure and scalable Joiner-Mover-Leaver (JML) identity governance process for the company's New York regional branch.

The project demonstrates how enterprise organizations automate and secure:

- Employee onboarding
- Employee department transfers
- Employee offboarding
- Access reassignment
- Security group governance
- Administrative segmentation
- Identity visibility
- Role-based access management

The environment was designed to simulate a real enterprise cloud identity governance architecture used by modern organizations.

---

<h2>🏢 Enterprise Scenario</h2>

<b>AeroMedia Global</b> recently expanded its operations into multiple regions and departments. As the company grew, the IT department began experiencing identity governance challenges including:

- Employees receiving incorrect access permissions
- Regional administrators having excessive privileges
- Manual onboarding delays
- Old employee accounts remaining active
- Lack of centralized governance
- Security risks caused by inconsistent role assignments

To solve these problems, the organization decided to redesign its identity management architecture using Microsoft Entra ID.

The primary goal was to build a centralized lifecycle governance system capable of securely managing employee identities from onboarding to offboarding.

---

<h2>🛠 Technologies and Services Used</h2>

| Technology | Purpose |
| :--- | :--- |
| Microsoft Entra ID | Identity and access management |
| Microsoft Azure Portal | Cloud administration platform |
| Administrative Units | Identity segmentation |
| RBAC | Role-based access control |
| Security Groups | Workforce access management |
| Microsoft 365 Groups | Collaboration management |
| Windows 11 Enterprise | Administrative workstation |
| Microsoft 365 Tenant | Enterprise cloud environment |

---

<h2>🧱 Lab Environment</h2>

| Component | Configuration |
| :--- | :--- |
| Identity Provider | Microsoft Entra ID |
| Tenant Type | Microsoft Entra ID Developer Tenant |
| Root Domain | `syskko.onmicrosoft.com` |
| Administrative Workstation | Windows 11 Enterprise |
| Browser Testing Mode | Incognito / Private Session |
| Privileged Account | Global Administrator |

---

<h2>🎯 Core Engineering Objectives</h2>

1. Build a centralized enterprise identity governance structure.
2. Create secure onboarding workflows for new employees.
3. Simulate employee department transfers.
4. Implement secure offboarding procedures.
5. Segment administration using Administrative Units.
6. Create enterprise workforce security groups.
7. Validate identity governance boundaries.
8. Reduce excessive administrative permissions.

---

# 🚀 Enterprise Implementation Walkthrough

---

<img src="images/step1.jpg"/> <br /><br />

Inside the tenant environment, I reviewed the existing users, groups, and identity configurations before building the lifecycle governance architecture.

---

## Step 1.1: Access the Identity Dashboard

Navigation Path:

```text
Identity → Overview
```

<img src="images/step2.jpg"/> <br /><br />

This dashboard provided visibility into:

- Tenant identity health
- Active users
- Administrative roles
- Security alerts
- Identity governance controls

---

## Step 1.2: Review Existing Users

Navigation Path:

```text
Identity → Users → All Users
```

<img src="images/step3.jpg"/> <br /><br />

I reviewed the current tenant identities to establish a clean baseline before creating the enterprise lifecycle environment.

This allowed me to identify:

- Existing accounts
- Role assignments
- User status
- Organizational structure

---

# Phase 2: Building Administrative Segmentation

The second phase focused on implementing Administrative Units.

Administrative Units allow organizations to separate identity administration responsibilities into smaller management boundaries.

This prevents regional administrators from gaining unnecessary global control over the tenant.

---

## Step 2.1: Create the New York Administrative Unit

Navigation Path:

```text
Identity → Administrative Units → Add
```

<img src="images/step4.jpg"/> <br /><br />

I created the following Administrative Unit:

| Setting | Value |
| :--- | :--- |
| Name | NY-Administrative-Unit |
| Description | New York regional identity management boundary |

<img src="images/step5.jpg"/> <br /><br />

This Administrative Unit became the primary regional governance container for the New York branch.

---

## Step 2.2: Validate Administrative Unit Deployment

After deployment completed successfully, I reviewed the Administrative Unit dashboard to verify:

- Administrative scope
- Identity isolation
- Regional segmentation
- Governance boundaries

<img src="images/step6.jpg"/> <br /><br />

The Administrative Unit was successfully deployed and operational.

---

# Phase 3: Creating Enterprise Workforce Groups

The next phase focused on building enterprise security groups for workforce access management.

Security groups simplify access management by allowing permissions to be assigned to groups instead of individual users.

---

## Step 3.1: Create the Regional Workforce Security Group

Navigation Path:

```text
Identity → Groups → New Group
```

<img src="images/step7.jpg"/> <br /><br />

I configured the following group:

| Setting | Value |
| :--- | :--- |
| Group Type | Security |
| Group Name | NY-Staff-Group |
| Description | Regional workforce access management group |

<img src="images/step8.jpg"/> <br /><br />

This security group was designed to centralize permissions for employees working inside the New York branch.

---

## Step 3.2: Add Users to the Security Group

I added enterprise users into the group to simulate regional workforce onboarding.

<img src="images/step9.jpg"/> <br /><br />

This structure allows administrators to:

- Assign permissions faster
- Reduce manual access assignment
- Improve governance consistency
- Simplify access reviews

---

# Phase 4: Creating Microsoft 365 Collaboration Groups

The next phase focused on collaboration governance.

Unlike security groups, Microsoft 365 groups provide collaboration capabilities including:

- Shared mailboxes
- Microsoft Teams integration
- Calendars
- SharePoint access
- Collaboration workspaces

---

## Step 4.1: Create the Marketing Collaboration Group

Navigation Path:

```text
Identity → Groups → New Group
```

<img src="images/step10.jpg"/> <br /><br />

I configured the following group:

| Setting | Value |
| :--- | :--- |
| Group Type | Microsoft 365 |
| Group Name | NY-Marketing-Group |
| Description | Marketing department collaboration group |

<img src="images/step11.jpg"/> <br /><br />

This group simulated a business collaboration environment for the marketing department.

---

## Step 4.2: Assign a Standard User as Group Owner

To reduce administrative workload, I delegated group ownership to a standard non-admin employee.

<img src="images/step12.jpg"/> <br /><br />

This demonstrates how organizations decentralize routine collaboration management while preserving centralized governance controls.

The delegated owner could:

- Add members
- Remove members
- Manage collaboration settings

The delegated owner could NOT:

- Modify tenant-wide settings
- Manage privileged identities
- Escalate privileges
- Access administrative controls

---

# Phase 5: Assigning Scoped Administrative Roles

The next phase focused on implementing Role-Based Access Control (RBAC).

Instead of granting tenant-wide administrative privileges, I scoped administrative permissions directly to the Administrative Unit.

This reduced the attack surface and enforced least privilege access.

---

## Step 5.1: Assign Scoped Administrative Permissions

Navigation Path:

```text
Administrative Units → Roles and Administrators
```

<img src="images/step13.jpg"/> <br /><br />

I assigned the following role:

| Role | Scope |
| :--- | :--- |
| Hybrid Identity Administrator | NY-Administrative-Unit |

<img src="images/step14.jpg"/> <br /><br />

This configuration ensured the regional administrator only controlled identities inside the New York Administrative Unit.

The administrator could NOT:

- Modify global tenant settings
- Manage identities outside the AU
- Escalate privileges globally
- Access unrelated business units

---

# Phase 6: Simulating Joiner Operations

This phase simulated employee onboarding.

The objective was to validate how new employees are provisioned into the environment with proper access assignments.

---

## Step 6.1: Create New Employee Accounts

Navigation Path:

```text
Identity → Users → New User
```

<img src="images/step15.jpg"/> <br /><br />

I created multiple employee identities representing different departments inside the New York branch.

Example users:

```text
Bob Jones
Sarah Lee
Greg Johnson
Bruno Capson
```

<img src="images/step16.jpg"/> <br /><br />

Each user was assigned:

- Department information
- Regional placement
- Group membership
- Identity governance scope

---

## Step 6.2: Add Employees into Workforce Groups

I added users into the correct security and collaboration groups based on their business responsibilities.

<img src="images/step17.jpg"/> <br /><br />

This simulated real enterprise onboarding workflows where new employees automatically receive access based on department placement.

---

# Phase 7: Simulating Mover Operations

The next phase simulated employee department transfers.

In enterprise environments, employees frequently change roles or departments.

Organizations must ensure identity permissions update correctly during transitions.

---

## Step 7.1: Modify Department Memberships

I updated user group memberships to simulate internal department movement.

<img src="images/step18.jpg"/> <br /><br />

This included:

- Removing users from old groups
- Assigning new department access
- Updating collaboration permissions
- Validating access inheritance

---

## Step 7.2: Validate Updated Access Permissions

After the transfer process completed successfully, I reviewed the user's effective access.

<img src="images/step19.jpg"/> <br /><br />

This confirmed:

- Old permissions were removed
- New permissions were applied
- Governance consistency was maintained

---

# Phase 8: Simulating Leaver Operations

The final lifecycle phase simulated employee offboarding.

Offboarding is one of the most critical identity governance processes because abandoned accounts create major security risks.

---

## Step 8.1: Disable Former Employee Accounts

Navigation Path:

```text
Identity → Users → Disable Account
```

<img src="images/step20.jpg"/> <br /><br />

I disabled former employee identities to simulate resignation or termination procedures.

---

## Step 8.2: Remove Group Memberships

I removed offboarded users from all enterprise groups.

<img src="images/step21.jpg"/> <br /><br />

This ensured:

- Access removal
- Collaboration revocation
- Governance cleanup
- Security enforcement

---

## Step 8.3: Validate Offboarding Controls

I verified the disabled accounts could no longer authenticate into the environment.

<img src="images/step22.jpg"/> <br /><br />

This confirmed the offboarding controls functioned correctly.

---

# Phase 9: Identity Governance Validation Testing

The final phase focused on validating the security architecture.

The purpose was to ensure users and administrators remained restricted to their assigned boundaries.

---

## Validation Test 1: Scoped Administrative Boundary Enforcement

Objective:

Verify that scoped administrators cannot manage identities outside their Administrative Unit.

<img src="images/step23.jpg"/> <br /><br />

Results:

- Regional administrators successfully managed users inside the AU
- Global tenant access remained blocked
- Cross-boundary management attempts failed

This confirmed Administrative Unit segmentation functioned correctly.

---

## Validation Test 2: Delegated Group Ownership Validation

Objective:

Verify that delegated business users could manage collaboration groups without receiving administrative privileges.

<img src="images/step24.jpg"/> <br /><br />

Results:

- Group owners successfully managed memberships
- Administrative controls remained unavailable
- Tenant-wide settings remained protected

This confirmed delegated collaboration governance worked correctly.

---

## Validation Test 3: Offboarding Security Validation

Objective:

Verify disabled employee accounts could no longer authenticate.

<img src="images/step25.jpg"/> <br /><br />

Results:

- Disabled users could not sign in
- Group memberships were removed
- Collaboration access was revoked

This confirmed lifecycle termination procedures functioned correctly.

---

# 🔒 Security Concepts Demonstrated

| Security Concept | Implementation |
| :--- | :--- |
| Least Privilege Access | Scoped RBAC assignments |
| Identity Segmentation | Administrative Units |
| Access Governance | Security Groups |
| Delegated Administration | Microsoft 365 Group Ownership |
| Identity Isolation | Regional boundaries |
| Lifecycle Governance | Joiner-Mover-Leaver workflows |
| Role Separation | Scoped administrative roles |
| Access Revocation | Controlled offboarding |

---

# 📊 Validation Matrix Results

| Validation Scenario | Result | Status |
| :--- | :--- | :---: |
| Scoped admin restricted to AU | Successful | PASS |
| Delegated owner limited to collaboration group | Successful | PASS |
| Offboarded employee blocked from access | Successful | PASS |
| Workforce group membership governance | Successful | PASS |
| Regional identity segmentation | Successful | PASS |

---

# 📚 Key Engineering Lessons Learned

## 1. Identity Governance Must Be Centralized

Managing identities manually across departments creates security gaps and operational inconsistency.

Centralized identity governance improves visibility and security control.

---

## 2. Administrative Segmentation Reduces Risk

Administrative Units significantly reduce the blast radius of compromised administrator accounts.

Regional administrators should never receive unnecessary global privileges.

---

## 3. Delegated Collaboration Improves Efficiency

Business departments can manage their own collaboration groups without requiring central IT intervention.

This reduces administrative workload while preserving governance security.

---

## 4. Offboarding Is a Critical Security Process

Former employee accounts create serious risks if they remain active.

Organizations must immediately disable identities and revoke access during employee exits.

---

# 🚧 Future Improvements

Future versions of this project will include:

- Dynamic group automation
- Conditional Access integration
- Privileged Identity Management (PIM)
- Automated HR synchronization
- Identity governance reporting
- Access review automation
- MFA enforcement policies
- Intune device compliance integration

---

# ✅ Final Project Outcome

This project successfully demonstrated a complete enterprise Joiner-Mover-Leaver identity lifecycle governance deployment using Microsoft Entra ID.

The final environment achieved:

- Secure onboarding workflows
- Controlled administrative segmentation
- Workforce access governance
- Delegated collaboration management
- Secure employee offboarding
- Centralized identity visibility
- Enterprise-grade governance boundaries

The implementation successfully simulated how modern organizations secure and manage employee identities across the full identity lifecycle.

---

## 🤝 Connect With Me

<p align="left">
<a href="https://linkedin.com/in/divine-oguamanam-a21765337" target="blank">
<img align="center" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/linkedin.svg" height="30" width="40" alt="LinkedIn Profile" />
</a>

<a href="https://twitter.com/syskko" target="blank">
<img align="center" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/twitter.svg" height="30" width="40" alt="Twitter Profile" />
</a>
</p>
