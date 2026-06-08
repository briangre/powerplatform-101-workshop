# Facilitator Guide

> This guide is for instructors delivering the Power Platform 101 Workshop.

## Pre-Workshop Checklist

### Environment Setup (1-2 days before)

- [ ] Provision a Power Platform **developer environment** (or trial)
- [ ] Create or assign user accounts for all attendees
- [ ] Assign **System Customizer** or **Environment Maker** security roles to all attendees
- [ ] Verify each attendee can sign in to [make.powerapps.com](https://make.powerapps.com) and see the environment
- [ ] Assign a **unique prefix** to each attendee (see Prefix Assignment below)
- [ ] Test the full workshop yourself end-to-end in the environment
- [ ] Verify Office 365 Outlook connector works for email notifications
- [ ] Prepare a slide deck or visual aids (see Lecture module for talking points)

### Prefix Assignment

Create a table mapping attendees to prefixes. Distribute this before or at the start of the workshop.

| Attendee | Prefix | Solution Name |
|----------|--------|---------------|
| Brian G. | `bg` | PP101 BCR - Brian G |
| Jane S. | `js` | PP101 BCR - Jane S |
| Alex M. | `am` | PP101 BCR - Alex M |
| ... | ... | ... |

**Rules for prefixes:**
- 2-4 lowercase letters
- Must be unique across all attendees
- Avoid common prefixes like `cr`, `new`, `sys`, `msdyn`

---

## Timing Guide

| Time | Module | Duration | Notes |
|------|--------|----------|-------|
| 0:00 | Lecture: Platform Overview | 30 min | Keep interactive — ask questions, show live demos |
| 0:30 | Environment Setup | 20 min | Walk around and help with login/publisher/solution issues |
| 0:50 | Lab 1: Dataverse | 40 min | This is the most critical lab — data model drives everything else |
| 1:30 | Lab 2: Model-Driven App | 40 min | Quick wins here — the app "just works" from Dataverse |
| 2:10 | **Break** | 10 min | |
| 2:20 | Lab 3: Canvas App | 45 min | Internal intake dashboard — gallery, forms, navigation with context |
| 3:05 | Lab 4: Power Automate | 30 min | Connection setup can be tricky — be ready to help |
| 3:35 | Lab 5: End-to-End Testing | 15 min | Celebrate successes — troubleshoot together |
| 3:50 | Wrap-Up & Q&A | 10 min | |

### Pacing Tips

- **If running behind:** Skip stretch goals, simplify form layouts, reduce sample data entry
- **If running ahead:** Encourage stretch goals, add the Approval connector in Power Automate, discuss production considerations
- **Biggest bottlenecks:** Environment setup (login issues), Dataverse column creation (naming/types), Canvas App formula errors

---

## Common Issues & Fixes

### Environment / Access

| Issue | Fix |
|-------|-----|
| Attendee can't see the environment | Re-assign the security role; have them sign out and back in |
| "You need a license" error | Verify trial or developer license is assigned |
| Multiple environments visible | Direct them to the correct environment name |

### Dataverse

| Issue | Fix |
|-------|-----|
| Table/column name conflicts | Verify prefix is being used consistently |
| Choice column values wrong | Show them how to edit the choice and re-save |
| Can't find table in data view | Navigate via Solutions → their solution → Tables |

### Canvas Apps

| Issue | Fix |
|-------|-----|
| Form shows "No item to display" | Set DefaultMode to `FormMode.New` |
| SubmitForm doesn't work | Check the form name matches the actual control name |
| Navigation doesn't work | Check screen names match Navigate() function arguments |
| Data card locked | Click the lock icon on the data card to unlock it |

### Power Automate

| Issue | Fix |
|-------|-----|
| Flow never triggers | Check: correct table? Change type = Added? Scope = Organization? |
| Connection authorization failed | Help them re-authenticate the Outlook and Dataverse connectors |
| Dynamic content missing | Ensure they're inserting from the correct trigger step |
| "Update a row" fails | Verify they're using the correct Row ID from dynamic content |

---

## Post-Workshop

### Cleanup

After the workshop:
1. Have attendees delete their flows (to stop email notifications)
2. Consider deleting all unmanaged solutions
3. Or reset the developer environment entirely

### Follow-Up Resources

Share the [Resources](../resources/README.md) page with attendees for continued learning.

### Feedback

Consider collecting feedback on:
- Pacing (too fast / just right / too slow)
- Which lab was most valuable
- What additional topics they'd like to learn
- Overall satisfaction
