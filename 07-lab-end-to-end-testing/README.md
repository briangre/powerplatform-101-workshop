# Lab 5: End-to-End Testing

> **Duration:** 15 minutes | **Type:** Hands-On Lab

## Learning Objectives

- Test the complete beneficiary change request process
- Validate data flows correctly between all components
- Identify and troubleshoot integration issues
- Understand how the components work together as a solution

---

## The Full Process

Here's what you've built — now let's test it end-to-end:

```
┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐    ┌──────────────────┐
│  INCOMING EMAIL   │    │   CANVAS APP     │    │  POWER AUTOMATE  │    │ MODEL-DRIVEN APP │
│  (from client)    │    │  (Intake Team)   │    │                  │    │   (Reviewer)     │
│                   │    │                  │    │                  │    │                  │
│  Client requests  │───▶│  Staff enters    │───▶│  Flow triggers:  │───▶│  Reviewer opens  │
│  a beneficiary    │    │  request from    │    │  • Send email    │    │  request         │
│  change           │    │  email into      │    │  • Update status │    │  • Reviews data   │
│                   │    │  system as Draft │    │    to "Under     │    │  • Approves or    │
│                   │    │  then Submits    │    │    Review"       │    │    rejects       │
│                   │    │  for Review      │    │                  │    │  • Adds notes    │
└──────────────────┘    └──────────────────┘    └──────────────────┘    └──────────────────┘
                              │                                               │
                              ▼                                               ▼
                        ┌──────────────────┐                           ┌──────────────────┐
                        │    DATAVERSE      │                           │    DATAVERSE      │
                        │  Row created as   │                           │  Status updated   │
                        │  "Draft" then     │                           │  to "Approved"    │
                        │  "Submitted"      │                           │  or "Rejected"    │
                        └──────────────────┘                           └──────────────────┘
```

---

## Test Script

Follow these steps in order. Check off each one as it passes.

### Test 1: Enter a New Request from an "Email"

Imagine you just received this email from a client:

> *"Hello, my name is Test User and I need to change the beneficiary on account ACCT-99999. The current beneficiary is Original Beneficiary. I'd like to change it to Updated Beneficiary, who is my spouse. This is part of an end-to-end test. My email is testuser@contoso.com. Thank you."*

1. Open your **Canvas App** (`{Prefix} - BCR Intake App`)
2. Click **＋ New Request**
3. Enter the details from the "email" above:

| Field | Value |
|-------|-------|
| Name / Request ID | `BCR-TEST-001` |
| Requestor Full Name | `Test User` |
| Requestor Email | `testuser@contoso.com` |
| Account Number | `ACCT-99999` |
| Current Beneficiary Name | `Original Beneficiary` |
| New Beneficiary Name | `Updated Beneficiary` |
| New Beneficiary Relationship | `Spouse` |
| Reason for Change | `End-to-end test of beneficiary change request process` |

4. Click **Save as Draft**

**Expected result:**
- [ ] Record saves successfully — notification appears
- [ ] You're returned to the dashboard
- [ ] New record appears in the gallery with "Draft" status

### Test 2: Submit the Request for Review

1. On the dashboard, click the `BCR-TEST-001` record you just created
2. Review the data for completeness
3. Click **Submit for Review**

**Expected result:**
- [ ] Record status changes to "Submitted"
- [ ] You're returned to the dashboard

### Test 3: Verify Dataverse Record

1. Go to [make.powerapps.com](https://make.powerapps.com) → **Tables**
2. Find your `{Prefix} Beneficiary Change Request` table
3. Open the data view

**Expected result:**
- [ ] Row exists with test data and status "Submitted" (then "Under Review" after flow runs)

### Test 4: Verify Flow Execution

1. Go to [make.powerautomate.com](https://make.powerautomate.com)
2. Find your `{Prefix} - BCR Notification Flow`
3. Click on **Run history**
4. Look for a recent run

**Expected result:**
- [ ] Flow run shows **Succeeded** status
- [ ] Each step (trigger, email, update) shows green checkmarks

### Test 5: Verify Email Notification

1. Check your email inbox (and spam/junk folder)

**Expected result:**
- [ ] Email received with subject containing `BCR-TEST-001`
- [ ] Email body contains the request details (requestor name, account, beneficiaries, reason)

### Test 6: Verify Status Update

1. Go back to the Dataverse table data view
2. Find the `BCR-TEST-001` record

**Expected result:**
- [ ] Request Status is now `Under Review` (updated by the flow)

### Test 7: Review in Model-Driven App

1. Open your **Model-Driven App** (`{Prefix} - BCR Review App`)
2. Navigate to the **Submitted Requests** or **All Active Requests** view
3. Open the `BCR-TEST-001` record

**Expected result:**
- [ ] Record opens with all data visible in organized sections
- [ ] Status shows "Under Review"

4. As a reviewer, update the record:
   - Change **Request Status** to `Approved`
   - Add **Reviewer Notes:** `Approved after verification. End-to-end test successful.`
   - Click **Save**

**Expected result:**
- [ ] Record saves successfully
- [ ] Status shows "Approved"

---

## Results Summary

| Test | Component | Pass/Fail |
|------|-----------|-----------|
| 1 | Canvas App → Enter & Save Draft | |
| 2 | Canvas App → Submit for Review | |
| 3 | Dataverse → Record Created | |
| 4 | Power Automate → Flow Ran | |
| 5 | Email → Notification Received | |
| 6 | Dataverse → Status Updated | |
| 7 | Model-Driven App → Review & Approve | |

### 🎉 If all tests pass — congratulations!

You've built a complete Power Platform solution that replaces a legacy email/spreadsheet process with:
- An internal intake dashboard for processing incoming requests (Canvas App)
- Automated notifications and status updates (Power Automate)
- Centralized data storage (Dataverse)
- An internal review and approval tool (Model-Driven App)

---

## Troubleshooting Common Issues

| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| Canvas app submits but no Dataverse record | Form not connected to correct table | Check form data source |
| Flow doesn't trigger | Wrong table or filter in trigger | Edit flow trigger settings |
| Email not received | Outlook connector issue | Re-authenticate the connection |
| Status stays "Submitted" | Flow failed on update step | Check flow run history for errors |
| Model-driven app shows no records | View filter excludes the record | Check view filter criteria |
| "Under Review" status not showing | Choice value mismatch | Verify choice option values match between flow and table |

---

## What Would Come Next?

In a real-world implementation, you would also consider:

- **Security roles** — who can submit vs. who can approve
- **Approval flows** — formal approve/reject with Power Automate Approvals connector
- **Audit trail** — track every status change with timestamps
- **SLA tracking** — monitor how long requests take to process
- **Power BI dashboard** — visualize request volumes, approval rates, processing times
- **Copilot Studio bot** — let requestors check status via chat
- **Power Pages portal** — external client self-service submission (instead of email intake)
- **Email parsing flow** — automatically create Dataverse records from incoming client emails using AI Builder
- **Environment strategy** — separate dev/test/production environments
- **DLP policies** — data loss prevention for connectors
- **Solution deployment** — managed solutions for production release
