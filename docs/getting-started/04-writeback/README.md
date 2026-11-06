# 4. Create a writeback

Turn the Opportunity tab into a **Savings Opportunity Tracker**: move from finding potential savings to recording and tracking actions.

For example, select a category with fragmented supplier spend, record a consolidation opportunity, assign an owner, and track its progress.

## What you will add

A saved opportunity has a category, business unit, title, owner, status, target savings amount, and notes. Users can create an opportunity and edit it later.

These are new operational records saved in the app's Rayfin-managed database, not changes to the Excel workbook or historical spend model. Target savings are user-entered estimates, separate from the model's illustrative benchmarks. Saving an opportunity does not automatically add it to the semantic model or the agent's Fabric IQ results.

## Prompt

Continue in the same chat with your existing app:

```text
Add a Savings Opportunity Tracker to the Opportunity tab in our existing app.

Let me select a category and business unit, then create an opportunity
with a title, owner, status, target savings in USD, and notes.
Use statuses New, In progress, and Completed.
Show saved opportunities in a list and let me edit them.

Persist these records in the app's Rayfin-managed database so they survive
a refresh. Use the generated Rayfin guidance for data modeling, permissions,
and write operations. Keep the existing sign-in and require authorized access.
Leave the source workbook and spend semantic model unchanged.

Match the existing design. Validate required fields and non-negative target
savings, show save progress and errors, and label target savings as estimates.
Test create, read, and update behavior, then deploy the updated app.
```

## Check the result

1. Create a test opportunity for a category shown in the app.
2. Save it, refresh the page, and confirm the record is still there.
3. Change its status and notes, save, and refresh again.
4. Confirm invalid entries are rejected and failed saves do not appear successful.
5. Confirm the original dashboard totals are unchanged.

You have demonstrated **writeback** when a user-entered change is saved to the backend and can be read back after a refresh, not just displayed temporarily in the browser.

[Previous: Change the visualization](../03-change-visualization/README.md)

[Next: Build a Foundry Agent](../../foundry-agent/README.md)

[Back to the hackathon](../../../README.md#lets-get-started)
