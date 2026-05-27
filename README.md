
<h1 align="center">🔐 Enterprise Identity Lifecycle Automation: Joiner-Mover-Leaver Pipeline in Microsoft Entra ID</h1>

<h3 align="center">
Built by <span style="color:#0078D4;">Divine Oguamanam</span>
</h3>

---

<h2>Project Overview</h2>

This project shows how to build a full identity lifecycle system in **Microsoft Entra ID** using **Microsoft Forms**, and **Power Automate**.

The business goal is simple.  
Remove manual work from identity management.

In many companies, HR sends emails to IT when a new hire joins, changes role, or leaves.  
That process is slow, noisy, and easy to break. It also creates security gaps.

This project models a real enterprise identity workflow for a fictional company called **AeroMedia Global**.  
It automates the full employee lifecycle with three clear flows:

- **Joiner**, for new hires
- **Mover**, for role changes and promotions
- **Leaver**, for offboarding

It also adds:

- **Custom Security Attributes** for classification
- **Dynamic group governance** for device filtering
- **Graph PowerShell automation** for bulk identity actions
- **Validation testing** to prove the design works

The result is a clean identity model that is faster, safer, and easier to manage.

<h3>Key Security Architecture Pillars</h3>

- **Least Privilege Access (PoLP):** Give each user only the access needed for the job.
- **Identity Lifecycle Automation:** Handle onboarding, transfers, and offboarding through flows.
- **Attribute-Based Access Control (ABAC):** Use user fields to drive access and governance.
- **Access Clean-Up:** Remove old access when people move or leave.
- **Security Validation:** Test each control to confirm it works.
- **Separation of Duties:** Keep HR input, IT actions, and access control separate.

<br />

<h2>Business Case</h2>

AeroMedia Global is a fast-growing digital media company.

Before automation, the company handled identity work by hand.  
That created problems like:

- Slow onboarding
- Wrong permissions
- Delayed access to tools
- Manual license mistakes
- Forgotten offboarding
- Orphaned accounts
- Compliance risk

When hiring scaled up, the IT queue got overloaded.  
New employees waited too long for access.  
Former employees sometimes kept access too long.  
That is a security problem and an operations problem at the same time.

This project solves that by shifting the company from manual ticket handling to an automated identity pipeline.

---

<h2>Technologies, Frameworks, and Tools</h2>

- **Identity Platform:** Microsoft Entra ID
- **Workflow Engine:** Microsoft Power Automate
- **Data Intake Tool:** Microsoft Forms
- **Admin Interface:** Microsoft Entra Admin Center
- **Automation Layer:** Microsoft Graph PowerShell SDK
- **Access Model:** Group-based access control
- **Security Method:** Attribute-based governance
- **Testing Method:** Manual validation in normal and private browser sessions

---

<h2>System & Lab Environment Baseline</h2>

- **Identity Cloud Provider:** Microsoft Entra ID developer tenant
- **Enterprise Root Domain:** `syskko.onmicrosoft.com`
- **Host Endpoint Platform:** Windows 11 Enterprise
- **Access Context:** Browser-based admin sessions and private browser test sessions
- **Automation Style:** Form-driven workflows with Graph PowerShell support
- **Validation Style:** Portal review, flow history checks, and user object checks

---

<h2>Core Engineering Objectives</h2>

1. Automate employee onboarding with a form-driven process.
2. Automate internal transfers and promotions.
3. Automate employee offboarding.
4. Use secure user attributes for identity classification.
5. Use dynamic device grouping for hardware trust boundaries.
6. Prove each phase with validation testing in Microsoft Entra ID.
7. Reduce manual work for HR and IT teams.
8. Reduce security risk from stale accounts and old access.
9. Build a portfolio project that looks like real enterprise identity work.

---

<h2>Identity Lifecycle Architecture</h2>

```text
[HR Form Submission]
        ↓
[Power Automate Flow]
        ↓
[Microsoft Entra ID]
        ↓
[User Attributes Updated]
        ↓
[Group Membership Changed]
        ↓
[Access Granted, Changed, or Removed]
