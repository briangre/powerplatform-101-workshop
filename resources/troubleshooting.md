# Troubleshooting Guide

## Quick Fixes for Common Issues

### 🔐 Access & Permissions

**"You don't have permission to access this environment"**
- Verify you're signed in with the correct account
- Ask your facilitator to assign the **Environment Maker** or **System Customizer** security role
- Try signing out completely and signing back in
- Clear browser cache and cookies for `*.powerapps.com`

**"You need a Power Apps license"**
- Your facilitator needs to assign a trial or developer license
- Developer environments come with included licenses — confirm the environment type

### 📊 Dataverse

**Table not showing in app or flow**
- Did you create the table inside your solution? Check Solutions → Your Solution → Tables
- Try refreshing the data sources in Power Apps Studio (Data panel → ... → Refresh)
- In Power Automate, try removing and re-adding the Dataverse connection

**Column values not saving**
- Check if the column is **Required** but has no value
- Verify the data type matches what you're entering
- For Choice columns, make sure you're selecting from the dropdown, not typing text

**"Duplicate key" or naming conflicts**
- Another attendee may have used the same schema name
- Always use your assigned prefix for all schema names
- Check with your facilitator for a new prefix if conflicts persist

### 📱 Canvas Apps

**"No item to display" on the form**
- Set the form's **DefaultMode** property to `FormMode.New`
- Make sure the data source is connected (check the Data panel)

**SubmitForm() does nothing**
- Verify the form control name: click the form, check its name in the property dropdown
- Check the **OnSuccess** and **OnFailure** properties for navigation or notifications
- Look at the App Checker (in the toolbar) for formula errors

**Navigate() doesn't work**
- Screen names are case-sensitive — verify the exact name
- Check for typos in the screen name within the Navigate() formula
- Ensure the target screen exists (check the Screens panel)

**Formula errors / red underlines**
- Click the error indicator to see the specific error message
- Common causes: wrong control name, wrong data type, missing parentheses
- Use the **App Checker** to see all errors in one place

### ⚡ Power Automate

**Flow never triggers**
- Verify the trigger settings: correct table, Change type = "Added", Scope = "Organization"
- If using row filters, double-check the OData filter syntax
- Make sure the flow is **turned on** (check the status on the flow details page)
- After saving changes, test the flow manually before waiting for automatic triggers

**"Connection not configured" or authorization error**
- Click on the connection name in the flow
- Click **Fix connection** or **Re-authenticate**
- Sign in again and authorize the connector

**Dynamic content is empty or missing**
- Make sure you're selecting from the correct step (the trigger, not another action)
- If the column was recently added to Dataverse, save and re-open the flow
- Try removing and re-adding the trigger to refresh the schema

**Email not received**
- Check spam/junk folder
- Verify the **To** address is correct
- Check the flow run details — did the email step succeed?
- Try sending to a different email address

### 🏢 Model-Driven Apps

**App shows no data**
- Check the view filters — your test data may not match the filter criteria
- Switch to the "All Active" or default view to see unfiltered data
- Verify data was actually saved in Dataverse (check the table data view directly)

**Form is missing fields**
- Open the form in the Form Designer
- Add missing columns from the column panel on the left
- Save and publish the form, then refresh the app

**App won't publish**
- Check for required columns that don't have default values
- Look for error messages in the App Designer
- Save the app first, then try publishing again

---

## General Tips

1. **When in doubt, refresh.** Many issues are resolved by refreshing the browser tab.
2. **Check the right environment.** Always confirm you're in the shared dev environment (top-right picker).
3. **Save frequently.** Power Apps Studio and Flow Designer can occasionally lose unsaved work.
4. **Use incognito/private mode** if you have multiple Microsoft accounts to avoid sign-in conflicts.
5. **Ask for help early.** Don't spend more than 5 minutes stuck — ask your facilitator or a neighbor.
