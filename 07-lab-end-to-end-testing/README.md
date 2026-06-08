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
│   CANVAS APP     │    │    DATAVERSE      │    │  POWER AUTOMATE  │    │ MODEL-DRIVEN APP │
│                  │    │                   │    │                  │    │                  │
│  Requestor       │───▶│  New row created  │───▶│  Flow triggers:  │    │  Reviewer opens  │
│  submits form    │    │  Status:Submitted │    │  • Send email    │    │  request         │
│                  │    │                   │    │  • Update status │    │  • Reviews data   │
│                  │    │  Status updated   │◀───│    to "Under     │    │  • Changes status │
│                  │    │  to Under Review  │    │    Review"       │    │  • Adds notes    │
└──────────────────┘    └──────────────────┘    └──────────────────┘    └──────────────────┘
```

---

## Test Script

Follow these steps in order. Check off each one as it passes.

### Test 1: Submit a New Request

1. Open your **Canvas App** (`{Prefix} - BCR Submission App`)
2. Click **Start New Request**
3. Fill in all fields with this test data:

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

4. Click **Submit Request**

**Expected result:**
- [ ] Confirmation screen appears
- [ ] No error messages

### Test 2: Verify Dataverse Record

1. Go to [make.powerapps.com](https://make.powerapps.com) → **Tables**
2. Find your `{Prefix} Beneficiary Change Request` table
3. Open the data view

**Expected result:**
- [ ] New row exists with test data
- [ ] Request Status should be "Submitted" initially (then "Under Review" after flow runs)

### Test 3: Verify Flow Execution

1. Go to [make.powerautomate.com](https://make.powerautomate.com)
2. Find your `{Prefix} - BCR Notification Flow`
3. Click on **Run history**
4. Look for a recent run

**Expected result:**
- [ ] Flow run shows **Succeeded** status
- [ ] Each step (trigger, email, update) shows green checkmarks

### Test 4: Verify Email Notification

1. Check your email inbox (and spam/junk folder)

**Expected result:**
- [ ] Email received with subject containing `BCR-TEST-001`
- [ ] Email body contains the request details (requestor name, account, beneficiaries, reason)

### Test 5: Verify Status Update

1. Go back to the Dataverse table data view
2. Find the `BCR-TEST-001` record

**Expected result:**
- [ ] Request Status is now `Under Review` (updated by the flow)

### Test 6: Review in Model-Driven App

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
| 1 | Canvas App → Submit | |
| 2 | Dataverse → Record Created | |
| 3 | Power Automate → Flow Ran | |
| 4 | Email → Notification Received | |
| 5 | Dataverse → Status Updated | |
| 6 | Model-Driven App → Review & Approve | |

### 🎉 If all tests pass — congratulations!

You've built a complete Power Platform solution that replaces a legacy paper/email process with:
- A modern submission form (Canvas App)
- Automated notifications (Power Automate)
- Centralized data storage (Dataverse)
- An internal review tool (Model-Driven App)

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
- **Power Pages portal** — external self-service submission
- **Environment strategy** — separate dev/test/production environments
- **DLP policies** — data loss prevention for connectors
- **Solution deployment** — managed solutions for production release
