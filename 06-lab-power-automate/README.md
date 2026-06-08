# Lab 4: Power Automate — Notifications & Automation

> **Duration:** 30 minutes | **Type:** Hands-On Lab

## Learning Objectives

- Create a cloud flow triggered by Dataverse
- Send notification emails automatically
- Update Dataverse records from a flow
- Understand triggers, actions, and conditions

---

## What We're Building

A **single cloud flow** that fires when a new beneficiary change request is submitted and:
1. Sends an email notification to a reviewer
2. Updates the request status to "Under Review"

This simulates the beginning of an automated review pipeline — replacing manual email forwarding and status tracking.

---

## Step-by-Step

### Step 1: Create the Cloud Flow

1. Open your solution (`PP101 BCR - {Your Name}`)
2. Click **+ New** → **Automation** → **Cloud flow** → **Automated**
3. Fill in:
   - **Flow name:** `{Prefix} - BCR Notification Flow` (e.g., `BG - BCR Notification Flow`)
   - **Trigger:** Search for `When a row is added` and select **Microsoft Dataverse — When a row is added, modified or deleted**
4. Click **Create**

### Step 2: Configure the Trigger

1. Set the trigger properties:
   - **Change type:** Added
   - **Table name:** `{Prefix} Beneficiary Change Requests` (your table)
   - **Scope:** Organization
2. Click **Show advanced options** (optional):
   - **Filter rows:** `{prefix}_requeststatus eq 100000001`  
     _(This filters to only "Submitted" status — value `100000001`)_
   
   > 💡 The filter is optional but recommended. Without it, the flow triggers on every new row regardless of status.

### Step 3: Add Action — Send an Email Notification

1. Click **+ New step**
2. Search for `Send an email` and select **Office 365 Outlook — Send an email (V2)**
3. Configure the email:

   - **To:** Your own email address (for testing)  
     _In production, this would be a reviewer distribution list or manager email_
   
   - **Subject:**
     ```
     New Beneficiary Change Request: [Click into dynamic content and select "Name"]
     ```
     Example result: `New Beneficiary Change Request: BCR-003`
   
   - **Body:**
     ```
     A new beneficiary change request has been submitted and requires review.

     Request ID: [Name]
     Requestor: [Requestor Full Name]
     Email: [Requestor Email]
     Account: [Account Number]
     
     Current Beneficiary: [Current Beneficiary Name]
     New Beneficiary: [New Beneficiary Name]
     
     Reason for Change:
     [Reason for Change]
     
     Submitted on: [Request Date]
     
     Please review this request in the BCR Review App.
     ```
   
   > 💡 Use **Dynamic content** (lightning bolt icon) to insert field values from the trigger.

### Step 4: Add Action — Update the Request Status

1. Click **+ New step**
2. Search for `Update a row` and select **Microsoft Dataverse — Update a row**
3. Configure:
   - **Table name:** `{Prefix} Beneficiary Change Requests`
   - **Row ID:** Select **Beneficiary Change Request** from Dynamic content (this is the unique identifier from the trigger)
   - **Request Status:** Select `Under Review`

### Step 5: Review Your Flow

Your flow should have 3 steps:

```
┌─────────────────────────────────────────────┐
│ TRIGGER: When a row is added                │
│ Table: Beneficiary Change Requests          │
│ Change type: Added                          │
└──────────────────┬──────────────────────────┘
                   ▼
┌─────────────────────────────────────────────┐
│ ACTION: Send an email (V2)                  │
│ To: your-email@contoso.com                  │
│ Subject: New BCR: {Name}                    │
│ Body: Request details                       │
└──────────────────┬──────────────────────────┘
                   ▼
┌─────────────────────────────────────────────┐
│ ACTION: Update a row                        │
│ Table: Beneficiary Change Requests          │
│ Status: Under Review                        │
└─────────────────────────────────────────────┘
```

### Step 6: Save and Test

1. Click **Save** in the top-right corner
2. Click **Test** in the top-right corner
3. Select **Manually** and click **Test**
4. Now, go to your **Canvas App** and submit a new beneficiary change request
5. Return to the flow — it should show a successful run
6. Check your email for the notification
7. Open your **Model-Driven App** and verify the record status changed to "Under Review"

---

## Understanding Flow Runs

After testing, explore the flow run history:

1. Go to the flow details page
2. Click on the **Run history** section
3. Click on a successful (or failed) run to see:
   - Input/output for each step
   - Duration
   - Error details (if any)

---

## ✅ Checkpoint

Before moving on, confirm:
- [ ] Your flow triggers when a new record is added to your Dataverse table
- [ ] An email notification is sent with request details
- [ ] The request status is automatically updated to "Under Review"
- [ ] The flow run history shows a successful run
- [ ] The record in Dataverse reflects the status change

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Flow doesn't trigger | Check: correct table selected? Scope set to Organization? Row filter correct? |
| Email not received | Check spam/junk folder. Verify the "To" address is correct. |
| Dynamic content is empty | Make sure you're selecting fields from the trigger step, not a different action |
| "Update a row" fails | Verify the Row ID uses the correct unique identifier from the trigger |
| Status doesn't update | Confirm you selected the correct choice value for "Under Review" |
| Connection error | Click on the connection name and re-authenticate if prompted |

---

## 🚀 Stretch Goals

If you finish early, try adding one or more of these to your flow:

### Add an Approval Step
1. Between the email notification and status update, add: **Approvals — Start and wait for an approval**
2. Set it to **Approve/Reject — First to respond**
3. Add a **Condition**: If approved → update status to "Approved"; If rejected → update status to "Rejected"

### Add a Teams Notification
1. Add a step: **Microsoft Teams — Post a message in a chat or channel**
2. Send a notification to a Teams channel when a new request comes in

### Add Error Handling
1. Click the **...** menu on the email action
2. Select **Configure run after**
3. Add a parallel branch that sends an error notification if the email fails
