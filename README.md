# Enterprise-Ticketing-System-Lab

### 1. Admin Center Environment Setup

![Admin Center Home](screenshots/01-admin-center-dashboard.png)

* **Objective:** Accessing and initializing the Zendesk Support Admin Center for instance `google-5200`.
* **Key Components:**
  * **Tenant Instance:** `google-5200.zendesk.com/admin`
  * **Navigation Hub:** Global administration entry point for configuring organization-wide business rules, routing, SLA matrices, and access permissions.
* **System Impact:** Serves as the central control plane for defining ITIL-compliant service desk workflows and platform architectures before ingesting user tickets.

---

### 2. Multi-Tier Support Group Configuration

![Support Groups Configuration](screenshots/02-support-groups-hierarchy.png)

* **Objective:** Establishing a tiered organizational support structure to segregate responsibilities between frontline help desk staff and senior engineering units.
* **Configured Groups:**
  * `Support` (Default Group, 1 Member): Default landing queue for general intake and Tier 1 triage.
  * `L1 IT Support` (0 Members): Dedicated frontline triage pool.
  * `L2 Desktop Engineering` (0 Members): Mid-tier endpoint and hardware troubleshooting queue.
  * `L3 Network Infrastructure` (0 Members): Specialized tier for core infrastructure, routing, VLAN, and major outage remediations.
* **Engineering Insight:** Setting up formal groups is a prerequisite for rule-based escalation and assignee relational integrity. Tickets cannot be escalated to specialized engineers without an isolated target group.

---

### 3. Incident Ingestion & Triage Queue Simulation

![Unsolved Tickets Queue](screenshots/03-unsolved-tickets-queue.png)

* **Objective:** Simulating real-world multi-incident ingestion to evaluate queue triage, default status assignment, and view categorization.
* **Managed Incidents Ingested:**
  * `Ticket #7`: *Floor 3 Manyata Office - Complete Wi-Fi Outage*
  * `Ticket #6`: *M365 Enterprise License Provisioning Request*
  * `Ticket #5`: *Outlook Client Stuck on 'Trying to Connect' Status*
  * `Ticket #4`: *GlobalProtect VPN Connection Timeout Error*
  * `Ticket #3`: *Windows Account Lockout - Urgent Password Reset*
* **Platform Behavior Observed:** All tickets initially defaulted to status `Open` with `Normal` priority via system default baseline rules (`Set tickets with no priority to normal`), illustrating the necessity for targeted priority classification and auto-escalation triggers.

---

### 4. P1 Incident Priority Elevation & Scope Assessment

![Ticket Priority Escalation](screenshots/04-ticket-priority-escalation.png)

* **Objective:** Escalating the Manyata facility wireless failure (`Ticket #7`) to Sev-1 / P1 status based on business impact.
* **Key Fields & Values:**
  * **Ticket Subject:** `Floor 3 Manyata Office - Complete Wi-Fi Outage`
  * **Impact Statement:** Complete loss of wireless connectivity on Floor 3 affecting 40+ employees, severing access to local network shares and VoIP infrastructure.
  * **Priority Field:** Manually upgraded from `Normal` to `Urgent`.
  * **AI / Sentiment Engine:** Tagged with `Negative` sentiment and `Connection issue` topic.
* **Engineering Insight:** Setting priority to `Urgent` is the prerequisite trigger for arming calendar-based P1 SLA targets (15-minute response, 2-hour resolution) defined in the corporate SLA framework.

* ---

### 5. Fast-Triage Inspection & Incident Classification

![Ticket Hover Inspection](./screenshots/05-agent-workspace-overview.ppg)

* **Objective:** Performing rapid triage using hover inspection cards directly within the ticket queue without context-switching.
* **Inspected Incident:** `Ticket #5` (*Outlook Client Stuck on 'Trying to Connect' Status*).
* **Technical Diagnostics Observed:**
  * **Symptom:** Desktop Microsoft 365 Outlook client frozen on the loading/connecting state.
  * **Root-Cause Isolation:** Web access (Outlook on the Web / OWA) verified operational, confirming Exchange mailbox and M365 licensing health; defect isolated to local desktop cached credentials or profile corruption.
* **Engineering Impact:** Enables frontline agents to quickly review diagnostic history and verify issue isolation before updating priority or routing to Tier 2.

---

### 6. ITIL Lifecycle State Segmentation (Open, Pending, Solved)

![Ticket Lifecycle States](./screenshots/06-ticket-hover-preview.png)

* **Objective:** Organizing ticket queues into discrete ITIL lifecycle states to maintain SLA accountability and workflow visibility.
* **Lifecycle States Managed:**
  * **Open Status:** Active tickets requiring internal troubleshooting (`Ticket #5`, `Ticket #6`, and the Sev-1 Manyata Outage `Ticket #7` set to `Urgent`).
  * **Pending Status:** `Ticket #4` (*GlobalProtect VPN Connection Timeout Error*) paused while awaiting end-user network test feedback.
  * **Solved Status:** `Ticket #3` (*Windows Account Lockout - Urgent Password Reset*) successfully fulfilled and marked resolved.
* **System Impact:** Moving tickets to `Pending` pauses requester wait timers where configured, while `Solved` seals the incident record and halts all active SLA countdowns.

---

### 7. Agent Workspace Dashboard & Queue Tracking

![Agent Workspace Overview](./screenshots/07-ticket-lifecycle-states.png)

* **Objective:** Monitoring incoming ticket volume, channel sources, and resolution metrics within the unified Agent Workspace.
* **Key Components:**
  * **Unified Queue View:** Real-time visibility into open incident streams across multiple enterprise applications (Outlook, GlobalProtect VPN, Microsoft 365, and Core Wireless Infrastructure).
  * **Workload Counters:** Active tracking showing 4 open/pending incidents and 1 ticket solved for the week.
* **Operational Insight:** Agent Workspace consolidates multi-channel support requests into a streamlined single-pane-of-glass queue, preventing ticket aging and backlog drift.
```

