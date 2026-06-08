# Lab 1: Dataverse Tables & Data Model

> **Duration:** 40 minutes | **Type:** Hands-On Lab

## Learning Objectives

- Create custom Dataverse tables
- Define columns with appropriate data types
- Create choice (option set) columns
- Understand table relationships
- Enter sample test data

---

## Business Scenario

A beneficiary change request captures the following information:
- **Who** is making the request (client/requestor info)
- **What** is being changed (current and new beneficiary details)
- **Why** the change is being made
- **Status** of the request as it moves through the process

---

## Step-by-Step

### Step 1: Open Your Solution

1. Go to [make.powerapps.com](https://make.powerapps.com)
2. Confirm you're in the **shared developer environment**
3. Click **Solutions** in the left navigation
4. Click into your solution (`PP101 BCR - {Your Name}`)

### Step 2: Create the Beneficiary Change Request Table

1. Inside your solution, click **+ New** → **Table** → **Table**
2. Fill in:
   - **Display name:** `{Prefix} Beneficiary Change Request`  
     (e.g., `BG Beneficiary Change Request`)
   - **Plural name:** `{Prefix} Beneficiary Change Requests`
   - **Schema name:** will auto-generate with your publisher prefix
   - **Primary column name:** Leave as `Name` (we'll use this for the Request ID/title)
3. Expand **Advanced options**:
   - Leave defaults for now
4. Click **Save**

### Step 3: Add Columns

Click into your new table, then go to the **Columns** tab. Add the following columns:

#### Requestor Information

| Display Name | Schema Name | Data Type | Required | Notes |
|---|---|---|---|---|
| Requestor Full Name | `{prefix}_requestorfullname` | Single line of text | Required | |
| Requestor Email | `{prefix}_requestoremail` | Single line of text (Email format) | Required | |
| Requestor Phone | `{prefix}_requestorphone` | Single line of text (Phone format) | Optional | |
| Account Number | `{prefix}_accountnumber` | Single line of text | Required | |

#### Current Beneficiary

| Display Name | Schema Name | Data Type | Required | Notes |
|---|---|---|---|---|
| Current Beneficiary Name | `{prefix}_currentbeneficiaryname` | Single line of text | Required | |
| Current Beneficiary Relationship | `{prefix}_currentbeneficiaryrelationship` | Single line of text | Optional | e.g., Spouse, Child, Parent |

#### New Beneficiary

| Display Name | Schema Name | Data Type | Required | Notes |
|---|---|---|---|---|
| New Beneficiary Name | `{prefix}_newbeneficiaryname` | Single line of text | Required | |
| New Beneficiary Relationship | `{prefix}_newbeneficiaryrelationship` | Single line of text | Optional | |
| New Beneficiary Date of Birth | `{prefix}_newbeneficiarydob` | Date Only | Optional | |

#### Request Details

| Display Name | Schema Name | Data Type | Required | Notes |
|---|---|---|---|---|
| Reason for Change | `{prefix}_reasonforchange` | Multiple lines of text | Required | |
| Request Date | `{prefix}_requestdate` | Date Only | Required | Default: today |
| Request Status | `{prefix}_requeststatus` | Choice | Required | See choices below |
| Reviewer Notes | `{prefix}_reviewernotes` | Multiple lines of text | Optional | |

### Step 4: Create the Request Status Choice Column

When creating the **Request Status** column:

1. Click **+ New column**
2. **Display name:** `Request Status`
3. **Data type:** Choice → **Choice**
4. Click **+ New choice**
5. Add the following options:

| Label | Value |
|-------|-------|
| Draft | 100000000 |
| Submitted | 100000001 |
| Under Review | 100000002 |
| Approved | 100000003 |
| Rejected | 100000004 |
| Completed | 100000005 |

6. **Default value:** `Draft`
7. **Required:** Yes
8. Click **Save**

### Step 5: Add Sample Data

> 💡 **Shortcut available:** If you'd rather import pre-built sample data instead of typing it manually, see the [Sample Data Import Guide](../resources/sample-data/README.md). A CSV file with 5 ready-to-import records is provided in the `resources/sample-data/` folder.

1. Click on the **Data** tab (or switch to the table's data view)
2. Add **3-4 sample rows** with fictional data:

**Example Row 1:**
| Field | Value |
|-------|-------|
| Name | `BCR-001` |
| Requestor Full Name | `Jane Smith` |
| Requestor Email | `jane.smith@contoso.com` |
| Account Number | `ACCT-10045` |
| Current Beneficiary Name | `John Smith` |
| Current Beneficiary Relationship | `Spouse` |
| New Beneficiary Name | `Sarah Smith` |
| New Beneficiary Relationship | `Daughter` |
| Reason for Change | `Updating beneficiary after divorce` |
| Request Date | Today's date |
| Request Status | `Submitted` |

**Example Row 2:**
| Field | Value |
|-------|-------|
| Name | `BCR-002` |
| Requestor Full Name | `Robert Chen` |
| Requestor Email | `robert.chen@contoso.com` |
| Account Number | `ACCT-20078` |
| Current Beneficiary Name | `Lisa Chen` |
| New Beneficiary Name | `Michael Chen` |
| New Beneficiary Relationship | `Son` |
| Reason for Change | `Adding adult child as primary beneficiary` |
| Request Date | Today's date |
| Request Status | `Draft` |

> 💡 **Reminder:** All data is fictional. Do not enter any real personal information.

---

## ✅ Checkpoint

Before moving on, confirm:
- [ ] Your Beneficiary Change Request table exists in your solution
- [ ] All columns are created with correct data types
- [ ] The Request Status choice column has all 6 options
- [ ] You have at least 2-3 sample data rows entered
- [ ] You can see your data in the table's data view

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Column won't save | Check for duplicate schema names — your prefix should make them unique |
| Can't find my table | Make sure you created it inside your solution, not at the environment level |
| Choice values don't appear | Save the choice set first, then apply it to the column |
| "Name" column confusion | The primary column ("Name") serves as the record identifier — use it for request IDs like `BCR-001` |

---

## 🚀 Stretch Goal

If you finish early:
- Add a **Business Rule** that makes "Reviewer Notes" required when the status is "Rejected"
- Add an **Attachment** column type for supporting documents
- Create a second table for **Beneficiary Change History** to track status changes over time
