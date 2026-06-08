# Lab 2: Model-Driven App — Review & Approval Experience

> **Duration:** 40 minutes | **Type:** Hands-On Lab

## Learning Objectives

- Create a model-driven app from your Dataverse table
- Customize forms for a review/approval workflow
- Create views to filter requests by status
- Understand the data-driven approach to app design

---

## Why Model-Driven First?

After creating your Dataverse tables, a model-driven app is the fastest way to get a working application. The app structure is **generated from your data model** — forms, views, and navigation are created automatically. This is ideal for internal users who need to review, manage, and process records.

---

## Step-by-Step

### Step 1: Create the Model-Driven App

1. Open your solution (`PP101 BCR - {Your Name}`)
2. Click **+ New** → **App** → **Model-driven app**
3. Fill in:
   - **Name:** `{Prefix} - BCR Review App` (e.g., `BG - BCR Review App`)
4. Click **Create**
5. You'll be taken to the **App Designer**

### Step 2: Add Your Table to the App

1. In the App Designer, you'll see a navigation panel on the left
2. Click **+ Add page**
3. Select **Dataverse table**
4. Click **Next**
5. Find and select your **{Prefix} Beneficiary Change Request** table
6. Click **Add**

### Step 3: Customize the Main Form

1. In the App Designer, click on your table page
2. Click the **Forms** section → select the **Main** form → click **Edit** (pencil icon) to open the Form Designer

#### Organize the Form into Sections

Create a logical layout for reviewers:

**Section 1: Requestor Information**
- Requestor Full Name
- Requestor Email
- Requestor Phone
- Account Number

**Section 2: Beneficiary Change Details**
- Current Beneficiary Name
- Current Beneficiary Relationship
- New Beneficiary Name
- New Beneficiary Relationship
- New Beneficiary Date of Birth

**Section 3: Request Information**
- Reason for Change
- Request Date
- Request Status

**Section 4: Review**
- Reviewer Notes

#### How to Organize Sections

1. Click **+ Component** in the form toolbar
2. Select **1-column section** or **2-column section**
3. Drag fields from the left panel into the appropriate sections
4. Rename sections by clicking on the section header
5. Rearrange columns by dragging them within or between sections

### Step 4: Customize the Form Header

1. Click on the form **header** area (top of the form)
2. Add these fields to the header for quick reference:
   - Request Status
   - Request Date
   - Requestor Full Name

### Step 5: Create Custom Views

Go back to the App Designer and click on your table's **Views**.

#### View 1: Submitted Requests (Default View)

1. Click **+ New view** (or edit the default Active view)
2. **Name:** `Submitted Requests`
3. Add columns: Name, Requestor Full Name, Account Number, Request Date, Request Status
4. Add a **filter:** Request Status **equals** `Submitted`
5. **Sort by:** Request Date (oldest first)
6. Save and close

#### View 2: All Active Requests

1. Click **+ New view**
2. **Name:** `All Active Requests`
3. Add columns: Name, Requestor Full Name, Account Number, Request Date, Request Status, Reason for Change
4. Add a **filter:** Request Status **does not equal** `Completed` AND Request Status **does not equal** `Rejected`
5. **Sort by:** Request Date (newest first)
6. Save and close

#### View 3: Completed & Rejected Requests

1. Click **+ New view**
2. **Name:** `Closed Requests`
3. Add columns: Name, Requestor Full Name, Request Date, Request Status, Reviewer Notes
4. Add a **filter:** Request Status **equals** `Completed` OR Request Status **equals** `Rejected`
5. Save and close

### Step 6: Configure the Site Map (Navigation)

1. Back in the App Designer, look at the left navigation
2. Your table should appear as a page
3. Rename the group/area if desired (e.g., "Beneficiary Management")

### Step 7: Save and Publish

1. Click **Save** in the top-right corner
2. Click **Publish**
3. Click **Play** (▶️) to open the app in a new tab

### Step 8: Test the App

1. In the app, you should see your views in the left navigation
2. Click **Submitted Requests** — you should see filtered records
3. Open a record — the form should display your organized sections
4. Try changing the **Request Status** from `Submitted` to `Under Review`
5. Add a **Reviewer Note**
6. Click **Save**

---

## ✅ Checkpoint

Before moving on, confirm:
- [ ] Your model-driven app opens and displays data
- [ ] The form has organized sections (Requestor, Beneficiary Change, Request Info, Review)
- [ ] At least 2 custom views are working (Submitted Requests, All Active Requests)
- [ ] You can open a record, change the status, add notes, and save
- [ ] The app is published

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Table doesn't appear when adding pages | Ensure the table was created inside your solution |
| Form fields are missing | Add the columns to the form manually from the left panel |
| View shows no records | Check your filter conditions — test data may not match the filter |
| App won't publish | Check for required fields that may not have default values |
| Can't edit records | Verify your security role has write access to the table |

---

## 🚀 Stretch Goals

If you finish early:
- Add a **Dashboard** showing request counts by status (use a chart)
- Add a **Business Rule** to make the form read-only when status is `Completed`
- Add the **Timeline** component to track activity history on each record
- Enable **Quick Find** search on Requestor Name and Account Number
