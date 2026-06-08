# Module 1: Environment Setup & Navigation

> **Duration:** 20 minutes | **Type:** Guided Setup

## Learning Objectives

- Navigate the Power Platform maker portal
- Understand environments and solutions
- Create a personal solution using proper naming conventions
- Set up a publisher with your assigned prefix

---

## ⚠️ Shared Environment — Naming Conventions

Since everyone is working in the **same developer environment**, we must use consistent naming to avoid conflicts.

Your facilitator will assign you a **unique prefix** (typically your initials or a short code).

### Naming Rules

| Asset | Naming Pattern | Example (prefix: `bg`) |
|-------|---------------|----------------------|
| **Publisher** | `{prefix}publisher` | `bgpublisher` |
| **Publisher Prefix** | `{prefix}` | `bg` |
| **Solution** | `PP101 BCR - {Your Name}` | `PP101 BCR - Brian G` |
| **Dataverse Table (Display)** | `{Prefix} Beneficiary Change Request` | `BG Beneficiary Change Request` |
| **Dataverse Table (Schema)** | `{prefix}_beneficiarychangerequest` | `bg_beneficiarychangerequest` |
| **Canvas App** | `{Prefix} - BCR Submission App` | `BG - BCR Submission App` |
| **Model-Driven App** | `{Prefix} - BCR Review App` | `BG - BCR Review App` |
| **Cloud Flow** | `{Prefix} - BCR Notification Flow` | `BG - BCR Notification Flow` |

> 💡 **Follow these naming conventions for every asset you create.** This prevents conflicts and makes cleanup easier.

---

## Step-by-Step

### Step 1: Navigate to Power Apps Maker Portal

1. Open your browser and go to [make.powerapps.com](https://make.powerapps.com)
2. Sign in with your provided credentials
3. In the **top-right corner**, click the environment picker
4. Select the **shared developer environment** provided by your facilitator

### Step 2: Create Your Publisher

1. In the left navigation, click **Solutions**
2. Look at any existing solution to understand publishers, or follow these steps:
   - We'll create the publisher as part of solution creation in the next step

### Step 3: Create Your Solution

1. Click **+ New solution**
2. Fill in:
   - **Display name:** `PP101 BCR - {Your Name}`
   - **Name:** (auto-generated)
   - **Publisher:** Click **+ New publisher**
     - **Display name:** `{Prefix} Publisher` (e.g., `BG Publisher`)
     - **Name:** `{prefix}publisher` (e.g., `bgpublisher`)
     - **Prefix:** `{prefix}` (e.g., `bg`)
     - Click **Save**
   - Select your new publisher
3. Click **Create**

### Step 4: Verify Your Solution

1. You should now see your solution in the solutions list
2. Click into your solution — it should be empty
3. This is where all your workshop assets will live

---

## Understanding the Maker Portal

Take a few minutes to explore:

- **Left navigation:** Apps, Flows, Tables, Solutions, Connections
- **Environment picker:** Top-right corner — always confirm you're in the right environment
- **Solutions view:** Where managed and unmanaged solutions are listed
- **Recent items:** Quick access to things you've worked on

---

## ✅ Checkpoint

Before moving on, confirm:
- [ ] You can access the shared developer environment
- [ ] You've created your personal publisher with your prefix
- [ ] You've created your solution (`PP101 BCR - {Your Name}`)
- [ ] Your solution is empty and ready for new components

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Can't see the environment | Ask facilitator to verify your security role assignment |
| "You don't have permission" | You need **Environment Maker** or **System Customizer** role |
| Publisher prefix already taken | Use a slightly different prefix (e.g., add a number: `bg1`) |
| Solution creation fails | Refresh the page and try again; check that publisher was saved |
