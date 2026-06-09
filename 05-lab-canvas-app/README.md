# Lab 3: Canvas App — Intake & Processing Dashboard

> **Duration:** 45 minutes | **Type:** Hands-On Lab

## Learning Objectives

- Create a Canvas App from scratch
- Build a gallery-based dashboard to browse Dataverse records
- Use navigation with context to pass data between screens
- Create an edit form for processing requests
- Use formulas to filter, update, and submit data

---

## The Business Context

In our beneficiary change request process, requests arrive from clients **via email** (or in a production scenario, through a Power Pages portal). An internal team member needs to:

1. **Enter** the request details from the email into the system
2. **Review** draft requests for completeness
3. **Submit** completed requests for formal review

The **Model-Driven App** (Lab 2) is designed for reviewers and approvers. This **Canvas App** is the day-to-day tool for the **intake team** — the people who receive the emails, enter the data, and prepare requests for review.

> 💡 **Why Canvas App for this?** Canvas apps give you pixel-perfect control over the layout and user experience. For an intake dashboard that an internal team uses all day, you want a streamlined, purpose-built interface — not a generic data entry form.

---

## Step-by-Step

### Step 1: Create the Canvas App

1. Open your solution (`PP101 BCR - {Your Name}`)
2. Click **+ New** → **App** → **Canvas app**
3. Fill in:
   - **App name:** `{Prefix} - BCR Intake App` (e.g., `BG - BCR Intake App`)
   - **Format:** Tablet
4. Click **Create**
5. The Canvas App Studio (Power Apps Studio) will open

### Step 2: Connect to Dataverse

1. In the left panel, click the **Data** icon (cylinder)
2. Click **+ Add data**
3. Search for your table: `{Prefix} Beneficiary Change Request`
4. Select it and click **Connect**

### Step 3: Design Screen 1 — Intake Dashboard

1. Rename the default screen to `scrDashboard`

#### Add a Header

1. Insert → **Rectangle** (or container)
   - Position at the top of the screen, full width
   - **Fill:** A dark color (e.g., `RGBA(0, 70, 127, 1)`)

2. Insert → **Text label** (on top of the rectangle)
   - **Text:** `Beneficiary Change Request — Intake Dashboard`
   - **Font size:** 24, **Bold:** true, **Color:** White, **Align:** Center

#### Add the "New Request" Button

3. Insert → **Button** (top-right area, near the header)
   - **Text:** `＋ New Request`
   - **OnSelect:**
   ```
   NewForm(frmRequest);
   Navigate(scrRequestForm, ScreenTransition.Fade)
   ```

#### Add a Gallery of Requests

4. Insert → **Vertical gallery**
5. Set the **Data source** (Items property) to your Beneficiary Change Request table:
   ```
   SortByColumns(
       Filter(
           '{Prefix} Beneficiary Change Requests',
           'Request Status' = 'Request Status ({Prefix} Beneficiary Change Requests)'.Draft
              || 'Request Status' = 'Request Status ({Prefix} Beneficiary Change Requests)'.Submitted
              || 'Request Status' = 'Request Status ({Prefix} Beneficiary Change Requests)'.'Under Review'
       ),
       "createdon",
       SortOrder.Descending
   )
   ```
   > 💡 Replace `{Prefix} Beneficiary Change Requests` with your actual table name. This shows active requests sorted by newest first.

6. Customize the gallery template to show key fields:
   - Click on the gallery and select the template (first row)
   - Add/edit labels inside the template:
     - **Title:** `ThisItem.Name` (the Request ID, e.g., BCR-001)
     - **Subtitle:** `ThisItem.'Requestor Full Name' & " — " & ThisItem.'Account Number'`
     - **Status:** `Text(ThisItem.'Request Status')`
   - Optionally add color-coded status indicators

7. Set the gallery's **OnSelect** property:
   ```
   Navigate(scrRequestForm, ScreenTransition.Fade)
   ```

#### Add a Request Count Label

8. Insert → **Text label** (below the header, above the gallery)
   - **Text:** `CountRows(Gallery1.AllItems) & " active requests"`
   - **Font size:** 12, **Italic:** true
   > Replace `Gallery1` with your actual gallery control name.

### Step 4: Design Screen 2 — Request Form (Edit/New)

1. Insert → **New screen** → **Blank**
2. Rename to `scrRequestForm`

#### Add a Header with Back Button

1. Insert → **Left arrow icon** (or Button)
   - **OnSelect:** `Navigate(scrDashboard, ScreenTransition.Fade)`
   - Position in the top-left

2. Insert → **Text label** (header)
   - **Text:** `If(frmRequest.Mode = FormMode.New, "New Request — Enter from Email", "Edit Request — " & frmRequest.LastSubmit.Name)`
   - **Font size:** 20, **Bold:** true

#### Add an Edit Form

3. Insert → **Edit form** (name it `frmRequest`)
4. Set the **Data source** to your Beneficiary Change Request table
5. Set the **Item** property to:
   ```
   Gallery1.Selected
   ```
   > Replace `Gallery1` with the name of your gallery on the Dashboard screen. This loads the selected record when editing. For new records, `NewForm()` (called from the dashboard) puts the form in "New" mode.

6. Resize the form to fill the screen (below the header)

#### Configure Form Fields

7. Click on the form and go to **Properties** → **Edit fields**
8. Remove system fields:
   - Remove: Created On, Modified On, Owner, Status Reason
9. Reorder fields logically:

   **Requestor Information:**
   - Requestor Full Name
   - Requestor Email
   - Requestor Phone
   - Account Number

   **Beneficiary Change:**
   - Current Beneficiary Name
   - Current Beneficiary Relationship
   - New Beneficiary Name
   - New Beneficiary Relationship
   - New Beneficiary Date of Birth

   **Request Details:**
   - Reason for Change
   - Request Date
   - Request Status

10. Set defaults for new records:
    - Unlock the **Request Date** data card → set its **Default** to `Today()`
    - Unlock the **Request Status** data card → set its **Default** to `'Request Status'.Draft`

### Step 5: Add Action Buttons

Add buttons below the form for the intake team's workflow:

#### Save as Draft Button

1. Insert → **Button**
   - **Text:** `Save as Draft`
   - **OnSelect:**
   ```
   SubmitForm(frmRequest)
   ```
   - This saves the record in its current state (Draft by default)

#### Submit for Review Button

2. Insert → **Button**
   - **Text:** `Submit for Review ▶`
   - **Fill:** A green or accent color to make it stand out
   - **OnSelect:**
   ```
   Patch(
       '{Prefix} Beneficiary Change Requests',
       frmRequest.LastSubmit,
       {'Request Status': 'Request Status'.Submitted}
   );
   SubmitForm(frmRequest)
   ```
   > This updates the status to "Submitted" and saves the record. Once submitted, the Power Automate flow (Lab 4) will pick it up.
   
   **Alternative simpler approach:** Unlock the Request Status data card, and before submitting, set its value:
   ```
   // Set status Update property to Submitted, then:
   SubmitForm(frmRequest)
   ```

#### Cancel Button

3. Insert → **Button**
   - **Text:** `Cancel`
   - **OnSelect:** `ResetForm(frmRequest); Navigate(scrDashboard, ScreenTransition.Fade)`

### Step 6: Wire Up Form Events

1. Select the **frmRequest** Edit Form
2. Set the **OnSuccess** property:
   ```
   Notify("Request saved successfully.", NotificationType.Success);
   Navigate(scrDashboard, ScreenTransition.Fade)
   ```
3. Set the **OnFailure** property:
   ```
   Notify("Error saving request. Please try again.", NotificationType.Error)
   ```

### Step 7: Save and Test

1. Click **Save** (top-right)
2. Click **Preview** (▶️ play button in top-right)
3. Test the following scenarios:

#### Test A: View Existing Requests
- The dashboard should show your sample data records
- Click on a record — the form should open with its data loaded

#### Test B: Create a New Request (from an email)
- Click **＋ New Request**
- Imagine you received this email from a client:
  > *"Hi, I'd like to change the beneficiary on my account ACCT-77001 from my former spouse Maria Lopez to my daughter Isabella Lopez (DOB 2005-04-12). My name is Carlos Lopez, email carlos.lopez@contoso.com. Thank you."*
- Enter the details from the "email" into the form
- Click **Save as Draft**
- Verify the record appears on the dashboard with "Draft" status

#### Test C: Submit a Request for Review
- Open the draft record you just created
- Click **Submit for Review**
- Verify the record status changes to "Submitted"
- Open your **Model-Driven App** and verify the request appears in the "Submitted Requests" view

---

## ✅ Checkpoint

Before moving on, confirm:
- [ ] Canvas App has 2 screens (Dashboard and Request Form)
- [ ] The dashboard gallery shows Dataverse records filtered to active requests
- [ ] Clicking a record opens it in the edit form
- [ ] "New Request" button opens a blank form
- [ ] "Save as Draft" creates/updates a record with Draft status
- [ ] "Submit for Review" changes the status to Submitted
- [ ] Submitted records appear in the Model-Driven App

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Gallery shows no records | Check the Items formula — verify table name and filter conditions |
| Clicking a gallery item doesn't load the form | Verify the form's `Item` property is set to `Gallery1.Selected` |
| Form shows "No item to display" | For new records, ensure `NewForm(frmRequest)` is called before navigating |
| "Save as Draft" creates a new record instead of updating | Check that the form's Item property is correctly linked to the gallery selection |
| Status doesn't change to Submitted | Verify you're patching with the correct choice value |
| Data source not found | Confirm the Dataverse table is connected in the Data panel |

---

## 🚀 Stretch Goals

If you finish early:
- Add a **status filter dropdown** on the dashboard so users can toggle between Draft, Submitted, All
- Add **conditional formatting** to the gallery: color-code items by status (e.g., Draft = gray, Submitted = blue, Under Review = orange)
- Add a **search bar** to filter the gallery by requestor name or account number:
  ```
  Filter(
      '{Prefix} Beneficiary Change Requests',
      StartsWith('Requestor Full Name', txtSearch.Text)
      || StartsWith('Account Number', txtSearch.Text)
  )
  ```
- Add a **record count by status** section on the dashboard using `CountIf()`
- Make the "Submit for Review" button **disabled** when required fields are empty:
  ```
  DisplayMode: If(
      IsBlank(DataCardValue_RequestorFullName.Text)
      || IsBlank(DataCardValue_ReasonForChange.Text),
      DisplayMode.Disabled,
      DisplayMode.Edit
  )
  ```
