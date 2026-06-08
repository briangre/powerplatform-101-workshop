# Module 0: Power Platform Overview

> **Duration:** 30 minutes | **Type:** Lecture

## Learning Objectives

By the end of this module, attendees will be able to:
- Describe the core components of Microsoft Power Platform
- Differentiate between Canvas Apps and Model-Driven Apps
- Explain what Dataverse is and why it matters
- Understand when to use Power Automate for process automation
- Recognize additional platform capabilities (Copilot Studio, Power Pages)

---

## Talking Points

### 1. What is Power Platform? (5 min)

- A suite of low-code/no-code tools for building business applications
- Part of the Microsoft ecosystem — integrates with Microsoft 365, Azure, Dynamics 365
- Four core pillars: **Power Apps**, **Power Automate**, **Power BI**, **Copilot Studio**
- Key value proposition: empower business users ("citizen developers") to build solutions without traditional development

**Key message:** *"Power Platform lets you replace spreadsheets, email chains, and paper forms with real applications — without writing code."*

### 2. Dataverse — Your Data Foundation (7 min)

- Cloud-based data platform built on Azure
- Structured storage with tables, columns, relationships, and business rules
- Built-in security model (row-level, field-level, role-based)
- Standard tables (Accounts, Contacts) and custom tables
- Why Dataverse over SharePoint lists or Excel:
  - Relational data support
  - Business logic enforcement
  - Security and compliance
  - Scalability
  - Native integration with all Power Platform components

**Demo idea:** Show a Dataverse table in the maker portal — highlight columns, data types, and relationships.

### 3. Power Apps — Canvas Apps vs. Model-Driven Apps (8 min)

#### Canvas Apps
- **Pixel-perfect control** — you design every screen, button, and layout
- Start from a blank canvas or template
- Great for: internal dashboards, task-specific tools, mobile experiences, custom UI/UX
- Data sources: Dataverse, SharePoint, SQL, Excel, APIs, and more
- Think: *"I want total control over the look and feel for a specific workflow"*

#### Model-Driven Apps
- **Data-first design** — the app structure comes from your Dataverse data model
- Automatically generates forms, views, dashboards
- Great for: internal business apps, case management, CRM-style workflows
- Built-in features: business rules, charts, timeline, related records
- Think: *"I want a professional business app quickly, driven by my data"*

#### When to Use Which?

| Scenario | Canvas App | Model-Driven App |
|----------|:---:|:---:|
| Internal intake/processing dashboard | ✅ | |
| Internal case management dashboard | | ✅ |
| Custom mobile form for field workers | ✅ | |
| Multi-entity relationship views | | ✅ |
| Branded, task-specific workflow tool | ✅ | |
| Quick CRUD app from Dataverse | | ✅ |

**Key message:** *"You don't have to choose one — many solutions use both together."*

### 4. Power Automate — Cloud Flows (5 min)

- Automate repetitive business processes
- **Triggers** → **Actions** → **Conditions** → **Outcomes**
- Common triggers: when a Dataverse row is created, when a form is submitted, on a schedule
- Common actions: send email, create approval, update a record, call an API
- Approval workflows: built-in approval connector with email/Teams notifications
- Types of flows: Automated, Instant, Scheduled

**Demo idea:** Show a simple "When a row is added → Send an email" flow.

### 5. Copilot Studio (3 min)

- Build AI-powered chatbots and virtual agents
- Integrates with Power Automate for backend actions
- Can be embedded in websites, Teams, and apps
- Use cases: FAQ bots, IT helpdesk, HR onboarding
- No-code conversation design with topics and trigger phrases

**Key message:** *"We won't build a bot today, but know that Copilot Studio extends your solutions with conversational AI."*

### 6. Power Pages (2 min)

- Build external-facing websites with data from Dataverse
- Use cases: customer portals, partner applications, public forms
- Secure data access with web roles and table permissions

**Key message:** *"Power Pages is how you expose your internal data and processes to external users — think customer self-service portals."*

---

## Transition to Hands-On Labs

> *"Now that you've seen the big picture, let's build something. Over the next 3 hours, we're going to create a Beneficiary Change Request process from scratch — imagine a client emails in a request, your internal team needs to enter it, route it for approval, and track it to completion. We'll start with the data model, then build the apps and automation."*

---

## Recommended Visual Aids

- Power Platform architecture diagram showing component relationships
- Side-by-side screenshot of a Canvas App vs. Model-Driven App
- Simple flow diagram of the beneficiary change request process we'll build
