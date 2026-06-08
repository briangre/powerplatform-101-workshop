# Sample Data

This folder contains pre-built sample data for the workshop labs.

## Files

| File | Description |
|------|-------------|
| `beneficiary-change-requests.csv` | 5 sample beneficiary change request records with various statuses |

## How to Import the CSV into Dataverse

> ⚠️ **You must complete [Lab 1: Dataverse Tables](../../03-lab-dataverse-tables/README.md) Steps 1–4 first** (create the table and all columns) before importing data.

### Step-by-Step

1. Download the `beneficiary-change-requests.csv` file from this folder
2. Go to [make.powerapps.com](https://make.powerapps.com) and confirm you're in the shared developer environment
3. Open your solution (`PP101 BCR - {Your Name}`)
4. Click into your **{Prefix} Beneficiary Change Request** table
5. Click the **Data** tab to open the data view
6. In the toolbar, click **Import** → **Import data from Excel**
7. Click **Upload** and select the downloaded CSV file
8. Power Apps will show a **Column Mapping** screen:
   - Map each CSV column to the corresponding Dataverse column in your table
   - Pay attention to the **Request Status** column — you may need to map the text values (`Draft`, `Submitted`, etc.) to your choice options
9. Click **Import**
10. Wait for the import to complete — you should see a success notification
11. Refresh the data view to confirm all 5 records were imported

### Column Mapping Reference

| CSV Column | Dataverse Column |
|------------|-----------------|
| Name | Name (Primary Column) |
| Requestor Full Name | {Prefix} Requestor Full Name |
| Requestor Email | {Prefix} Requestor Email |
| Requestor Phone | {Prefix} Requestor Phone |
| Account Number | {Prefix} Account Number |
| Current Beneficiary Name | {Prefix} Current Beneficiary Name |
| Current Beneficiary Relationship | {Prefix} Current Beneficiary Relationship |
| New Beneficiary Name | {Prefix} New Beneficiary Name |
| New Beneficiary Relationship | {Prefix} New Beneficiary Relationship |
| New Beneficiary Date of Birth | {Prefix} New Beneficiary Date of Birth |
| Reason for Change | {Prefix} Reason for Change |
| Request Date | {Prefix} Request Date |
| Request Status | {Prefix} Request Status |

### Troubleshooting

| Issue | Fix |
|-------|-----|
| Import button not visible | Make sure you're in the table data view, not the column designer |
| Column mapping errors | Verify all columns exist in your table before importing |
| Status values don't map | Manually update the Request Status after import if needed |
| Date format issues | The CSV uses `YYYY-MM-DD` format — this should map automatically |
| Duplicate records after re-import | Delete existing sample rows first, then re-import |

> 💡 **Tip:** If the import tool gives you trouble, it's perfectly fine to enter the sample data manually — there are only 5 rows.
