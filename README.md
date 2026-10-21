# Marceline Studios Shopify Developer Assessment

## Part A — Repair & Complete the Theme Section

### Changes made

- Kept the existing section settings and Online Store 2.0 block schema.
- Used the `title` setting for the section heading.
- Used each benefit block's `label` and `description` settings for its content.
- Added a condition so a benefit description is not rendered when it is blank.
- Added a CTA condition that checks whether the CTA is enabled and has both a label and a URL.
- Added a responsive layout that changes from three columns to a single column below 768px.

### Validation

I opened the section in Shopify and confirmed that it renders. I also checked the mobile layout and CTA behavior in the cases I tested.

## Part B — Production Troubleshooting

### First two hypotheses

1. Rapid clicks may trigger overlapping add-to-cart requests. If an earlier request finishes after a later one, its response could overwrite the badge with an older quantity. I’d check the browser’s Network tab to compare request order, response order, and the quantity displayed after each response.

2. The badge may be reading the wrong value or may not be refreshed from the latest cart state. I’d compare the add-to-cart response with the cart page’s item count and the badge. If the response has the right count but the badge does not, the issue is likely in how the page updates the badge.

### Minimal safe fix

I’d update the badge using the cart quantity returned by Shopify after a successful add. To handle overlapping requests, I’d either process them one at a time or make sure an older response cannot overwrite a newer result. If a request fails, I’d leave the badge unchanged and show the error.

```text
When an item is added:
  send the add-to-cart request
  if it succeeds:
    update the badge with the returned cart item count
  if it fails:
    keep the current badge count and show an error
```

### Regression checks

1. Add one item and confirm the badge matches the cart.
2. Add several items quickly and confirm the final badge shows the correct total.
3. Simulate a failed add and confirm the badge does not increase incorrectly.

## Part C — Professional Judgment

### 01. Problem-solving

I’d stop repeating approaches that have already failed, then narrow the issue down to recent changes and a small reproducible case. I’d share what I know, what I’ve tried, and the remaining risk with the PM as soon as the deadline is at risk, not wait until I have a complete fix. Then I’d agree on the next step, such as a smaller safe fix, more investigation time, or moving the deadline.

### 02. Ownership / QA

I’d tell the PM exactly what the mobile defect is and how it affects the page, then check how serious it is and whether there’s a safe fix before review. I’d either fix and verify the mobile layout or make sure the PM knows clearly that it remains unresolved.

### 03. Parallel priorities

I’d compare the two tasks by deadline, customer impact, and what happens if each one is delayed, then confirm priorities with the PM rather than silently choosing. I’d explain what I can finish today, what will need to move, and when I can provide the next update.

### 04. AI-assisted work

I used AI assistance while working through this assessment, including reviewing the Liquid conditions and organizing these written answers. I checked the suggested changes against the section settings and tested the section in Shopify; I would not use a suggestion I could not explain or verify.

### 05. Client recovery

I’d acknowledge the client’s frustration, reproduce the defect, and check which users or pages are affected before proposing a fix. I’d give the client clear progress updates and an honest estimate, then verify the fix and explain what changed. If I caused the issue, I’d own that and focus on restoring confidence through reliable follow-through.

### 06. Honest billing / teamwork

For hourly work, I’d report the four hours actually worked, even if the estimate was ten; for a fixed per-page fee, I’d follow the agreed fee and scope. If a teammate disagreed, I’d review the contract or billing rules with them and raise it with the PM if we still couldn’t agree, rather than changing the report to avoid a difficult conversation.

## Tools

- Shopify Theme Editor / preview for section checks.
- AI assistance for reviewing Liquid logic and drafting the written responses.
