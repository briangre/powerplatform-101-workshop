# Lab 3: Canvas App — Request Submission Form

> **Duration:** 45 minutes | **Type:** Hands-On Lab

## Learning Objectives

- Create a Canvas App from scratch
- Design a multi-screen submission form
- Connect to Dataverse as a data source
- Use formulas to submit and validate data
- Create a user-friendly experience for request submission

---

## Why Canvas App?

While the model-driven app serves internal reviewers, the **Canvas App** provides a clean, branded submission experience for requestors. Canvas apps give you pixel-perfect control over the UI — every button, layout, and color is yours to design.

---

## Step-by-Step

### Step 1: Create the Canvas App

1. Open your solution (`PP101 BCR - {Your Name}`)
2. Click **+ New** → **App** → **Canvas app**
3. Fill in:
   - **App name:** `{Prefix} - BCR Submission App` (e.g., `BG - BCR Submission App`)
   - **Format:** Tablet (or Phone — your choice)
4. Click **Create**
5. The Canvas App Studio (Power Apps Studio) will open

### Step 2: Connect to Dataverse

1. In the left panel, click the **Data** icon (cylinder)
2. Click **+ Add data**
3. Search for your table: `{Prefix} Beneficiary Change Request`
4. Select it and click **Connect**

### Step 3: Design Screen 1 — Welcome / Home Screen

1. Rename the default screen to `scrHome`
2. Add the following controls:

#### Title & Instructions

1. Insert → **Text label**
   - **Text:** `Beneficiary Change Request`
   - **Font size:** 28, **Bold:** true
   - Position at the top-center of the screen

2. Insert → **Text label** (below the title)
   - **Text:** `Use this form to submit a request to change the beneficiary on your account. Please have your account number and beneficiary information ready.`
   - **Font size:** 14
   - **Auto height:** true

#### Start Button

3. Insert → **Button**
   - **Text:** `Start New Request`
   - **OnSelect:** `Navigate(scrRequestForm, ScreenTransition.Fade)`
   - Style it with a color that fits your design

### Step 4: Design Screen 2 — Request Form

1. Insert → **New screen** → **Blank**
2. Rename to `scrRequestForm`

#### Add an Edit Form

1. Insert → **Edit form**
2. Set the **Data source** to your Beneficiary Change Request table
3. Resize the form to fill most of the screen
4. The form will auto-populate with fields from your table

#### Configure Form Fields

1. Click on the form and go to **Properties** → **Edit fields**
2. Remove fields that shouldn't be on the submission form:
   - Remove: Reviewer Notes, Created On, Modified On, Owner
3. Keep and reorder these fields:
   - Requestor Full Name
   - Requestor Email
   - Requestor Phone
   - Account Number
   - Current Beneficiary Name
   - Current Beneficiary Relationship
   - New Beneficiary Name
   - New Beneficiary Relationship
   - New Beneficiary Date of Birth
   - Reason for Change

4. Lock the following fields or set default values:
   - **Request Status:** Set the default to `Draft` and hide or lock this field
   - **Request Date:** Set the default to `Today()` and lock this field

#### Set Form Mode

Set the form's **DefaultMode** property to:
```
FormMode.New
```

### Step 5: Add Submit and Cancel Buttons

#### Submit Button

1. Insert → **Button** (below the form)
2. **Text:** `Submit Request`
3. **OnSelect:**
```
SubmitForm(Form1);
```
> Replace `Form1` with the actual name of your Edit Form control.

#### Cancel Button

1. Insert → **Button**
2. **Text:** `Cancel`
3. **OnSelect:** `Navigate(scrHome, ScreenTransition.Fade)`

### Step 6: Design Screen 3 — Confirmation

1. Insert → **New screen** → **Blank**
2. Rename to `scrConfirmation`
3. Add controls:

#### Success Message

1. Insert → **Text label**
   - **Text:** `✅ Your beneficiary change request has been submitted successfully!`
   - **Font size:** 22
   - Center on screen

2. Insert → **Text label**
   - **Text:** `You will receive updates on the status of your request.`

#### Return Button

3. Insert → **Button**
   - **Text:** `Submit Another Request`
   - **OnSelect:**
   ```
   ResetForm(Form1);
   Navigate(scrRequestForm, ScreenTransition.Fade)
   ```

4. Insert → **Button**
   - **Text:** `Return Home`
   - **OnSelect:** `Navigate(scrHome, ScreenTransition.Fade)`

### Step 7: Wire Up Form Submission

1. Select your **Edit Form** on the Request Form screen
2. Set the **OnSuccess** property:
```
Navigate(scrConfirmation, ScreenTransition.Fade)
```
3. Set the **OnFailure** property:
```
Notify("There was an error submitting your request. Please try again.", NotificationType.Error)
```

### Step 8: Auto-Set Status to Submitted

To automatically set the status when the form is submitted, update the **Request Status** data card:

1. Unlock the **Request Status** data card (click the lock icon)
2. Find the **Update** property of the data card
3. Set it to the "Submitted" choice value:
```
'Request Status'.Submitted
```

> This ensures every new request is automatically set to "Submitted" status.

### Step 9: Save and Test

1. Click **Save** (top-right)
2. Click **Preview** (▶️ play button in top-right)
3. Test the full flow:
   - Click "Start New Request" on the home screen
   - Fill in all required fields with fictional data
   - Click "Submit Request"
   - Verify you're taken to the confirmation screen
4. Go to your **Model-Driven App** and verify the new record appears with status "Submitted"

---

## ✅ Checkpoint

Before moving on, confirm:
- [ ] Canvas App has 3 screens (Home, Request Form, Confirmation)
- [ ] The form connects to your Dataverse table
- [ ] Submitting the form creates a new record in Dataverse
- [ ] The status is automatically set to "Submitted"
- [ ] Navigation between screens works
- [ ] The submitted record appears in your Model-Driven App

---

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Data source not found | Confirm you're connected to the correct Dataverse table in the Data panel |
| Form shows "No item to display" | Set the form's DefaultMode to `FormMode.New` |
| Submit creates record but with blank status | Unlock the status data card and set the Update property |
| OnSuccess doesn't fire | Make sure you used `SubmitForm(FormName)` with the correct form name |
| Columns missing from form | Click Edit fields on the form and add the missing columns |

---

## 🚀 Stretch Goals

If you finish early:
- Add **input validation** (e.g., require email format, minimum length for Reason)
- Add a **banner or logo** to the home screen for branding
- Add a **gallery screen** that shows the user's previously submitted requests
- Add a **loading spinner** while the form is submitting using a variable:
  ```
  UpdateContext({isSubmitting: true});
  SubmitForm(Form1);
  ```
