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

<h2>Enterprise Scenario</h2>

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

<h2>Technologies and Services Used</h2>

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

<h2> Core Engineering Objectives</h2>

1. Build a centralized enterprise identity governance structure.
2. Create secure onboarding workflows for new employees.
3. Simulate employee department transfers.
4. Implement secure offboarding procedures.
5. Segment administration using Administrative Units.
6. Create enterprise workforce security groups.
7. Validate identity governance boundaries.
8. Reduce excessive administrative permissions.

---

# 1. Project Overview & Business Case

---

The Scenario <br />

This project models the production implementation of an automated Identity Lifecycle Management (ILM) pipeline for AeroMedia Global, a mid-sized, rapidly scaling digital media platform.
Previously, AeroMedia handled all employee onboarding and offboarding manually. HR would email the IT operations queue when a new hire was signed, and a helpdesk administrator would manually provision the user account in Microsoft Entra ID, assign software licenses, and add them to individual security groups.

The Problem <br />

As monthly hiring scaled up by 400%, this manual approach completely broke down:

- Operational Bottlenecks: It took an average of 48 hours post-hire for engineers to receive access to essential development repos, halting engineering velocity. 
- Licensing Waste: Inactive or incorrect attributes led to human error during manual license assignments, costing thousands in unutilized Microsoft 365 seat licenses. 
- Critical Security Vulnerabilities: Former employees were not being offboarded cleanly. Orphaned accounts remained active weeks after termination, leaving a massive backdoor open for potential data breaches and failing basic compliance audits (SOC 2 / ISO 27001). 

The Solution Architecture  <br />

To eliminate these business risks, I architected a Zero-Touch Identity Pipeline using an Attribute-Based Access Control (ABAC) model. By simulating an authoritative HR data source, the infrastructure automatically handles the birth, movement, and termination of corporate identities based purely on user metadata attributes (like Department and Employment Status).

[HR Source Intake] ──> [Automation Engine] ──> [Entra ID Directory] ──> [Dynamic Group Security Gates] 

This engineering strategy shifts the IT department from a reactive ticket-handling queue into a strict, secure, self-healing access governance system. 


---
2. Phase 1: Constructing the Authoritative Data Source (HR Intake Portal)
---

In an enterprise deployment, identity lifecycles must begin at an authoritative source of truth (such as Workday or BambooHR). To simulate this engine without a massive enterprise budget, I built a structured intake portal using Microsoft Forms.
This form acts as the data-entry gate for the HR department. Every question inside this form maps directly to a specific schema attribute within our cloud directory space

- First Name maps to the givenName attribute. 
- Last Name maps to the surname attribute. 
- Department maps to the department attribute (the core variable driving our automated group logic).
- Start Date maps to the temporal execution triggers. 

<img src="Images/step 1.jpg"/> <br /><br />

To start, I opened Microsoft Forms to make our hiring portal. I did not use any of the ready-made templates, such as "Registration" or "Questionnaire." Instead, I clicked the New Form button to start with a completely blank page. This lets me choose the exact questions I need for our automation project without any extra stuff getting in the way. 

<img src="Images/step 2.jpg"/> <br /><br />

<img src="Images/step 3.jpg"/> <br /><br />

- I added a required text field for the First Name. This maps directly to the givenName attribute inside Microsoft Entra ID. 
- I added a required text field for the Last Name. This maps directly to the surname attribute inside Microsoft Entra ID. 
- I added a text field for the Desired Corporate Email. The automation engine will use this to set up the user's main login name (User Principal Name or UPN) in the cloud. 

<img src="Images/step 4.jpg"/> <br /><br />

<img src="Images/step 5.jpg"/> <br /><br />

I created a Department selection field. This is the most important parameter because our dynamic security groups will use this specific text to automatically grant the employee the appropriate software licenses and access rights. 

<img src="Images/step 6.jpg"/> <br /><br />

<img src="Images/step 7.jpg"/> <br /><br />

I added an Employee Start Date field using the date picker tool. This allows the lifecycle workflows to schedule exactly when the account setup should trigger before the user arrives. 

<img src="Images/step 8.jpg"/> <br /><br />

I replaced the default form name with HR Onboarding Intake Portal. This provides a clear, professional title for the internal HR staff who will use this interface to submit new hire data. 

The onboarding form is hosted entirely within the Microsoft 365 cloud environment. All configuration changes, form parameters, and field requirements are saved automatically in real-time to the cloud tenant database, ensuring the intake portal is immediately ready to pass data to our automation tools. 

---
Starting the Cloud Flow in Power Automate 
---
- In my new browser tab, I went to make.powerautomate.com. 

<img src="Images/step 9.jpg"/> <br /><br />

<img src="Images/step 10.jpg"/> <br /><br />

- Look at the left sidebar menu, and I clicked on the + Create button.
- On the page that opens, I clicked on the card named Automated cloud flow.

---

Naming the Flow and Choosing the Trigger 

---

- A window will pop up asking for a Flow name and a trigger. 

<img src="Images/step 11.jpg"/> <br /><br />

I named the automation pipeline Automated Onboarding - User Provisioning Pipeline and chose When a new response is submitted from Microsoft Forms as my starting trigger. This ensures the system acts as a listener, waiting for HR to send a new hire's data. 

<img src="Images/step 12.jpg"/> <br /><br />

<img src="Images/step 13.jpg"/> <br /><br />

Inside the Power Automate cloud flow designer, the initial trigger card displays an error because it needs an exact data target. To fix this, I navigated to the Form ID parameter drop-down list on the left panel and selected our saved HR Onboarding Intake Portal. This configuration establishes a real-time data link, instructing the automation engine to monitor this specific portal and execute the pipeline the exact second an HR administrator submits a new employee's information.

<img src="Images/step 14.jpg"/> <br /><br />

The initial trigger only signals that a form was submitted, but it cannot read the actual input values. To extract the text data entered by HR, I used the Add an action function, searched for the Microsoft Forms connector, and selected Get response details. This step allows the automation flow to read the specific responses inside the form fields. 

---
Configuring the Data Reader (Get Response Details) 
---

Once I clicked Get response details, a new configuration card opened up on the left side of my screen with two blank fields: Form ID and Response ID. 

<img src="Images/step 15.jpg"/> <br /><br />

---

Mapping the Data Fields 

---

<img src="Images/step 16.jpg"/> <br /><br />

After adding the Get response details action, I configured it by selecting the HR Onboarding Intake Portal under the Form ID parameter.
In the Response ID field, I used the dynamic content menu to insert the unique Response ID token. This configuration ensures that whenever the flow runs, the engine extracts the exact text data (First Name, Last Name, and Department) from that specific new hire submission.

---

Add the Entra ID Account Creation Step

---
Now that the flow can read the HR data, I am ready to add the final part: telling Microsoft Entra ID to create the actual user account

<img src="Images/step 17.jpg"/> <br /><br />

With the intake data successfully extracted from the form response, the next step in the pipeline is to send this information directly to our cloud directory.
I added a new action, searched for the Microsoft Entra ID connector, and selected the Create user action. This step serves as the final execution gate, translating our raw form inputs into an active enterprise user identity account.

<img src="Images/step 18.jpg"/> <br /><br />

Once I select Create user, a new panel opens on the left with a list of empty boxes. I must map the form fields to these boxes. When I click inside any of these boxes, a Dynamic content menu will pop up on the side showing the questions from the form.

---
Mapping Attributes to the Cloud Schema 
---

<img src="Images/step 19.jpg"/> <br /><br />

Inside the Create user configuration block, I mapped the incoming form parameters to the official Microsoft Entra ID schema attributes using the dynamic content routing engine: 

- Given Name was mapped to the dynamic First Name form token.
- Surname was mapped to the dynamic Last Name form token.
- Department was mapped to the dynamic Department form token. This is the critical variable that drives the automated group assignments.
- Password was hardcoded with a secure temporary string (WelcomeAeroMedia2026!) that applies to all newly created directory entries before their first login, forcing a reset. 

---

Saving The Cloud Flow and Activating the Automation 

---

<img src="Images/step 20.jpg"/> <br /><br />

After fully mapping all the directory attributes, I clicked Save in the upper-right corner of the Power Automate designer. This saves the logic to the cloud tenant and automatically turns the flow on, putting it into a live listening state. 

---
Running the Onboarding Test 
---
Now I will simulate HR hiring a real person

<img src="Images/step 21.jpg"/> <br /><br />

<img src="Images/step 22.jpg"/> <br /><br />

<img src="Images/step 23.jpg"/> <br /><br />

<img src="Images/step 24.jpg"/> <br /><br />

To test the end-to-end automation pipeline, I navigated to the Microsoft Forms dashboard and opened the HR Onboarding Intake Portal. I clicked the Preview button in the upper-right control panel to switch from design mode to the active user interface.
From this live view, I filled out a test case entry for a new hire named "Simon Jackson" assigned to the "Engineering" department and clicked Submit. This submission acts as the live trigger event to kick off our automated provisioning flow in Power Automate

---
Checking the Flow Run (Testing Results)
---

<img src="Images/step 25.jpg"/> <br /><br />

<img src="Images/step 26.jpg"/> <br /><br />

I navigated back to the Power Automate dashboard to review the Run History. The log shows a status of Succeeded, proving that the engine successfully intercepted the form submission, extracted the string data, and communicated with the directory without any authentication or schema errors. 

---
The Final Proof (Checking Microsoft Entra ID)
---

<img src="Images/step 27.jpg"/> <br /><br />

<img src="Images/step 28.jpg"/> <br /><br />

As a final validation gate, I logged into the Microsoft Entra Admin Center and checked the global user directory. The account Simon Jackson was successfully created with all corporate attributes intact, confirming that my zero-touch provisioning pipeline is fully operational.

---
3. Phase 2:The "Mover" Pipeline (Internal Transfer / Promotion) 
---

The Mover phase happens when an existing employee changes roles, switches departments, or gets a promotion. For example, if John moves from Sales to Engineering, he shouldn't keep his access to sales databases, but he does need access to engineering tools. 

How it works in a real IT environment: 

- The Trigger: HR updates the employee’s department or job title in Microsoft Forms or HR software.
- The Automation: Power Automate detects the change, updates their Department field in Microsoft Entra ID, automatically removes them from old department groups, and adds them to their new department groups. 

The Mover alignment represents the mid-lifecycle phase of an employee, triggered by internal transitions such as department transfers, promotions, or geographic relocations. In a fully realized identity lifecycle framework, a separate Power Automate pipeline monitors changes to existing directory objects.
When HR submits a role-change notification, the automation engine dynamically updates the user's target attributes (such as Job Title, Manager, or Department) within Microsoft Entra ID. This modification automatically triggers dynamic group membership rules, stripping away legacy permissions and provisioning new, role-appropriate access privileges. This enforces the security principle of Least Privilege.
In an enterprise environment, a "Mover" flow requires a way to identify which existing employee is moving, and what their new details are. I will build this by creating a dedicated Internal Transfer Form and then connecting it to a new Power Automate flow that updates Microsoft Entra ID. 

---
Create the "Internal Transfer" Form 
---

Before building the automation, I need an intake portal specifically for employees who are changing roles. 

- I will enter New Form and name it: HR Internal Transfer & Promotion Portal. 

<img src="Images/step 29.jpg"/> <br /><br />

To support mid-lifecycle identity changes, I designed a second entry portal using Microsoft Forms titled HR Internal Transfer & Promotion Portal. Unlike the initial onboarding form, this portal requires the administrator to input the employee's existing Corporate Email as a unique identifier. It captures transition metrics, including New Job Title and New Department, to serve as the authoritative data payload for the transfer pipeline. 


---
Initialize the Mover Flow in Power Automate 
---

Now I will create a brand-new automation engine specifically for handling internal transfers. 

- Open Power Automate (make.powerautomate.com). 
- I will click + Create on the left menu, then select Automated cloud flow. 

<img src="Images/step 30.jpg"/> <br /><br />

<img src="Images/step 31.jpg"/> <br /><br />

- I named this flow: Automated Mover Pipeline - Role Transitions.
- Search for the trigger: When a new response is submitted (Microsoft Forms), select it. 

I initialized a separate automated cloud flow named Automated Mover Pipeline - Role Transitions. I bound the execution trigger to our newly created HR Internal Transfer & Promotion Portal. This decouples the "Joiner" logic from our "Mover" logic, ensuring that role transitions do not accidentally run user-creation scripts. 

---
Add the Data Reader (Get Response Details) 
---
Just like the Joiner flow, the system needs an action step to extract the answers typed into the transfer form. 

<img src="Images/step 32.jpg"/> <br /><br />

<img src="Images/step 33.jpg"/> <br /><br />

I appended the Get response details action card to parse incoming transfer payloads. By linking the Form ID to the transfer portal and mapping the unique dynamic Response ID token, the pipeline isolates the specific submission data containing the moving employee's new corporate assignment details. 

---
Add the "Update User" Action for Entra ID 
---
- Click the blue circular + (Plus) button under your "Get response details" card and click Add an action. 
- type: Microsoft Entra ID
- select: Update user.

<img src="Images/step 34.jpg"/> <br /><br />


---

How to configure the card parameters:

---
<img src="Images/step 35.jpg"/> <br /><br />

- User ID (or Principal Name): Click inside this box. From the Dynamic Content pop-up menu, select the token for Employee Corporate Email (from your Form questions). This tells Entra ID exactly who is moving.
- Job Title: I clicked inside this box and selected the New Job Title token from the form questions.
- Department: I clicked inside this box and selected the New Department token from the form questions. 

To execute the lifecycle modification, I added the Update user action from the Microsoft Entra ID connector. I mapped the User ID parameter to the incoming form token Employee Corporate Email.
Next, I mapped the New Job Title and New Department tokens to their corresponding target directory fields. When executed, this action modifies the existing directory object attributes in real-time without interrupting active user authentication sessions.

My Mover pipeline is complete! Now i will save it and test it out. 

<img src="Images/step 36.jpg"/> <br /><br />

<img src="Images/step 37.jpg"/> <br /><br />

Go to the HR Internal Transfer & Promotion Portal form, click Preview, and submit a transfer request. 

<img src="Images/step 38.jpg"/> <br /><br />

- Crucial: For the Employee Corporate Email, type in the email address of a user in a group. So I picked Myria from the  marketing group myriasanchez@syskko.onmicrosoft.com 

<img src="Images/step 39.jpg"/> <br /><br />

- New Job Title: Type Operations 
- New Department: Operations
- Manager Name/Email: SimonJackson@syskko.onmicrosoft.com 

<img src="Images/step 40.jpg"/> <br /><br />

---
Verification: Checking the Results 
---
Once I hit submit, the Power Automate pipeline will catch the data and update her profile in the background. Here is how to verify it worked: 

<img src="Images/step 41.jpg"/> <br /><br />

Myria Sanchez remained in the marketing group because Microsoft Entra ID treats User Profiles (text attributes) and Security Groups (access containers) as completely separate systems. Updating her department metadata to "Operations" did not trigger an automatic movement from her statically assigned groups. To bridge this gap, explicitly configured automation steps are required to programmatically remove the user from the legacy NY-Marketing-Group and append them to the target NY-Operations-Group, fully completing the lifecycle transfer. 

---
Remove her from the Marketing Group 
---
Because NY-Operations-Group is a Microsoft 365 group (which is tied to Microsoft Teams), I can use the Microsoft Teams connector or the Office 365 Groups connector in Power Automate to move her. 

<img src="Images/step 42.jpg"/> <br /><br />

<img src="Images/step 43.jpg"/> <br /><br />

---
Add to the next Group
---

<img src="Images/step 44.jpg"/> <br /><br />

<img src="Images/step 45.jpg"/> <br /><br />

Issue Observed: During the configuration of the Microsoft Teams (Add a member to a team) action card, the target group NY-Operations-Group did not appear in the standard automated dropdown selection menu. This occurs because the directory container was provisioned as a Microsoft 365 Group but had not yet been fully initialized with a Microsoft Teams workspace front-end.
Resolution Strategy: To bypass this connector limitation, I referenced the master groups directory within the Microsoft Azure/Entra ID console and extracted the unique Object ID for the group: 97ba7d1e-4cf7-41ae-91b0-b9a6f5c8a7ed.
Inside the Power Automate designer, I bypassed the standard dropdown menu by selecting Enter custom value and manually binding the explicit Object ID into the execution field. This forces the cloud workflow engine to query the backend directory directly by its absolute identifier rather than relying on Teams app discovery, successfully routing the automation payload and resolving the provisioning block.

---
Add the Correct Group Action 
---
- Click the blue circular + (Plus) button right below my Remove member from group card.
- In the search box, type: Office 365 Groups 
- Look through the actions list and select Add member to group 
- I will configure the card parameters exactly like this:
- Group ID:  NY-Operations-Group.
- User ID: Click inside this box and select the Employee Corporate Email token from the Form questions. 

Now I went back to the Microsoft form and filled it out the form again 

HR Internal Transfer & Promotion Portal. 

So it is transferred now to the Operation Group

<img src="Images/step 46.jpg"/> <br /><br />

I will try Sarah Lee and shift her from the Marketing Group to the Operations Group 

<img src="Images/step 47.jpg"/> <br /><br />

Went back to the Microsoft Forms preview page, filled the form, and submitted.

<img src="Images/step 48.jpg"/> <br /><br />

I went back to my Power Automate Run History. Because Sarah is actually starting in Marketing and moving to Operations, the flow will process all cards seamlessly and give me a solid green Succeeded checkmark. 

<img src="Images/step 49.jpg"/> <br /><br />

<img src="Images/step 50.jpg"/> <br /><br />

A system check in Microsoft Entra ID shows that this automation works perfectly. A live test on Sarah Lee proves that the system handles both removing and adding permissions at the same time without any manual work from IT.
When the form was submitted, the automation immediately went to the old marketing group and completely removed Sarah Lee from the list. This keeps our data secure by making sure she no longer has access to files she doesn't need, while leaving the rest of the marketing team untouched.
At the same time, the system added her to the new department. Checking the operations group shows that Sarah Lee is now successfully listed next to her new teammates. She now has instant, day-one access to all of the operations files, chat channels, and tools. This successful move proves that the automation is safe, working, and ready to use.

---

4. The Leaver Story: Saying Goodbye to Marketing 

---

Let's meet Justin Blakeley. He was one of the two members left in our NY-Marketing-Group after Sarah Lee moved away.
Justin has decided to leave the company to pursue a new opportunity. In a standard, non-automated company, this creates a major security risk. An HR manager might tell IT that Justin is leaving, but an overworked IT admin might forget to remove him from his email groups, forget to block his sign-in, or leave his account active for weeks. This is called "Security Sprawl," where an ex-employee still has keys to the digital kingdom.
With this new Leaver Pipeline, the moment HR fills out the Offboarding Form, a clean, automated sweep happens instantly:

- Justin’s profile status is changed to "Inactive." 
- His Microsoft account is immediately locked, so he can no longer log in. 
- He is completely stripped of all his group memberships (like NY-Marketing-Group), so he instantly loses access to company files.

The Step-by-Step Blueprint

I am going to build this as a brand-new flow since it triggers from a completely different event (an offboarding form instead of a transfer form). Here is my plan:

Prep the Form 

- Go to Microsoft Forms and create an HR Employee Offboarding Portal.
- It only needs one main question: Employee Corporate Email. 

<img src="Images/step 51.jpg"/> <br /><br />

<img src="Images/step 52.jpg"/> <br /><br />

---
Create the Flow Trigger 
---

<img src="Images/step 53.jpg"/> <br /><br />

- I went to Power Automate, created an Automated Cloud Flow, and chose the When a new response is submitted trigger (connected to your new Offboarding Form). 

<img src="Images/step 54.jpg"/> <br /><br />

<img src="Images/step 55.jpg"/> <br /><br />

<img src="Images/step 56.jpg"/> <br /><br />

<img src="Images/step 57.jpg"/> <br /><br />

---
Add the "Update user" Card (To Lock Their Account) 
---
This step will instantly block the leaving employee from logging back into company systems. 

<img src="Images/step 58.jpg"/> <br /><br />

<img src="Images/step 59.jpg"/> <br /><br />

<img src="Images/step 60.jpg"/> <br /><br />

---
Add the "Remove member from group" Card 
---

<img src="Images/step 61.jpg"/> <br /><br />

<img src="Images/step 62.jpg"/> <br /><br />

I will save it 

To run this live test for the Leaver pipeline, I just need to submit a response to the new offboarding form and check the results.

<img src="Images/step 63.jpg"/> <br /><br />

<img src="Images/step 64.jpg"/> <br /><br />

- Refresh the page after about 10–15 seconds. The entry says Succeeded with a bright green checkmark

---
Verify the Security Changes in Azure / Entra ID 
---

Now I will get to verify that the security sweep actually worked. Open the Microsoft Azure / Entra ID tab and check two things: 

Check 1: Is his account locked? 


<img src="Images/step 65.jpg"/> <br /><br />

Look at his profile properties. His Account Status or Account Enabled field should now say No (or show a blocked status), meaning he can no longer log in. 

---
Check 2: Is he removed from the group? 
---

<img src="Images/step 66.jpg"/> <br /><br />

---
Project Conclusion: Identity Lifecycle Automation
---
This project successfully builds a complete, automated system to manage employees from the day they are hired to the day they leave the company. By using Microsoft Forms and Power Automate to control Microsoft Entra ID (Azure), I have created a safe and fast way to handle user accounts without any manual work from the IT team.
The project proves that all three stages of the employee cycle work perfectly:

- The Joiner Pipeline: Automatically creates brand-new user accounts for fresh hires, sets their job titles, and puts them into the correct initial email and security groups. 
- The Mover Pipeline: Instantly handles internal job changes. When an employee switches departments, the system automatically changes their job profile, removes them from their old department group, and grants them access to their new department tools. 
- The Leaver Pipeline: Safely offboards departing employees. The moment a manager flags someone as leaving, the automation instantly locks their account so they can no longer log in and strips away all their group permissions. 

By replacing manual IT tasks with this smart automation, the company completely avoids human mistakes, stops ex-employees from keeping access to company files, and ensures new hires have everything they need to start working on day one. The system is secure, reliable, and ready for full business use. 

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

# Validation Matrix Results

| Validation Scenario | Result | Status |
| :--- | :--- | :---: |
| Offboarded employee blocked from access | Successful | PASS |
| Workforce group membership governance | Successful | PASS |
| Regional identity segmentation | Successful | PASS |

---

# 📚 Key Engineering Lessons Learned

## 1. Identity Governance Must Be Centralized

Managing identities manually across departments creates security gaps and operational inconsistency.

Centralized identity governance improves visibility and security control.


---

## 2. Delegated Collaboration Improves Efficiency

Business departments can manage their own collaboration groups without requiring central IT intervention.

This reduces administrative workload while preserving governance security.

---

## 3. Offboarding Is a Critical Security Process

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
