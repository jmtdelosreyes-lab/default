**To:** Willie [Accounting Team Lead] <willie@[domain]>
**Cc:** Accounting Team
**Subject:** Burkhart Dental – AR Tax Removal Request: Investigation Results, Blockers, and Items Requiring Your Input

Hi Willie and team,

Thank you for sending over the 06/19 AR aging file with the notes on the Burkhart Dental items flagged for sales tax removal. Before we proceed with any updates in NetSuite, we completed a full investigation of the 110 transactions against live NetSuite data and the accounting period status. Below is a summary of what we found, the blockers we hit, and the items we need your confirmation on before any changes are made.

Full detail (per-invoice classification, tier assignments, period feasibility, and recommended actions) is in the attached workbook: **Burkhart_Tax_Removal_Analysis.xlsx**. All amounts in the Executive Summary tab are formula-driven from the Detail tab, so any reclassification you make to the Tier column will flow through automatically.

---

### 1. Customers in scope

Only two customer records are affected:

- **314 – Burkhart Dental Supply Company** (parent) – already flagged `taxable = F` in NetSuite. Most invoices on this entity have no tax line.
- **1727 – Heath Hollis** (child of 314) – currently flagged `taxable = T`. This must be updated to `taxable = F` with the exemption certificate attached **before** any invoice edits, otherwise AVATAX will recalculate tax on save and undo the changes.

---

### 2. Classification of the 110 transactions

We grouped the 103 invoices and 7 credit memos into the following tiers, based on comparing the unpaid balance against the actual sales tax on each NetSuite invoice:

| Tier | Description | Count | Unpaid $ | Tax $ |
|---|---|---:|---:|---:|
| **T1 – Clean Removal** | Unpaid balance exactly equals the sales tax. Removing tax zeroes the invoice. | 55 | 789.86 | 789.86 |
| **T2 – Fully Unpaid w/ Tax** | Tax present but no customer payment yet. | 20 | 5,040.11 | 334.17 |
| **T3 – Partial-pay Mismatch** | Partial payment, unpaid ≠ tax. (INV681804, INV687698) | 2 | 83.65 | 48.98 |
| **T0 – No Tax on Invoice** | No tax line in NetSuite – tax removal not applicable. | 26 | 3,700.99 | 0.00 |
| **CM – Pending Application** | Credit memos awaiting your application instructions. | 5 | (140.19) | – |
| **CM – Recently Issued** | Recently issued credit memos (informational). | 2 | (102.60) | – |
| **Total** | | **110** | **9,371.82** | **1,173.01** |

The total ties to the $9,371.82 outstanding on your source file.

**Please confirm the tier breakdown and amounts above before we proceed.**

---

### 3. Blockers identified

**A. Accounting period status (most critical)**

All 55 T1 "clean removal" invoices fall in periods that are currently closed and AR-locked in NetSuite:

| Period range | Status | T1 Invoices |
|---|---|---:|
| Aug 2025 – Mar 2026 | Closed + AR Locked | 45 |
| Apr 2026 | Open, but AR Locked | 10 |
| May – Jun 2026 | Fully Open | 0 |

Direct invoice edits in closed or AR-locked periods will be blocked by NetSuite. None of the T1 invoices sit in an open editable period today.

**B. AVATAX (Avalara) integration**

All Heath Hollis (1727) invoices are AVATAX-calculated. Saving an edited invoice triggers a recommit to Avalara, and if the customer is still marked taxable, the tax line will be re-added automatically. The taxable flag update on customer 1727 must therefore happen before any edits.

**C. Sales tax filing**

Confirmed with your team that the relevant period sales tax has not yet been remitted/filed, so no amended-return obligation. This removes one significant compliance concern.

**D. Payment application anomalies**

Two of the partial-pay invoices show payment-application irregularities that need eyeballing in the NetSuite UI before any tax adjustment:
- **INV681804** – $42.56 unpaid; payment PYMT942981 of $594.40 applied, but balance does not reconcile.
- **INV687698** – $41.09 unpaid; payment PYMT943619050 of $526.73 applied, similar pattern.

---

### 4. Recommended approach

Since the accounting team has indicated a preference for editing the invoices directly (rather than issuing credit memos – which we agree conceptually fits, as there is no return of goods, only a tax reconciliation), we present two paths. **Either is operationally workable; the choice depends on whether the controller is willing to reopen periods.**

**Option A – Direct Edit (accounting's stated preference)**

1. Update customer 1727 record: `taxable = F` and attach the exemption certificate.
2. Controller temporarily reopens the affected periods (Aug 2025 – Mar 2026) and unlocks AR for Apr 2026, ideally one batch at a time, after-hours.
3. We edit each invoice to remove the tax line (or change per-line tax codes to a non-taxable code so AVATAX does not re-add it).
4. Periods are re-locked and re-closed immediately after.

   Pros: Original invoice is corrected; AR aging shows the change against the original period.
   Cons: Requires controller-level period reopen; touches multiple closed months; any other user with AR access during the unlock window could post unrelated entries; previously distributed reports for those months may become stale.

**Option B – Credit Memo posted to current open period (recommended alternative)**

For each affected invoice, issue a credit memo equal to the tax amount only, dated in the current open period (Jun 2026), applied to the original invoice.

   Pros: No period unlock required; works for all 55 T1 invoices in a single batch; full audit trail preserved (CM is linked to original invoice); reversible if needed; AVATAX has no opportunity to recommit on the original; no risk of unrelated edits leaking into reopened periods.
   Cons: Two-line entry per invoice (original invoice + CM) instead of a single edited invoice; the tax-liability reversal posts to Jun 2026 rather than the original period (acceptable since none of these were filed yet).

We lean toward **Option B** for the 55 T1 invoices given the period-lock situation, but it is your team's call. The GL impact is functionally the same – reduction of Sales Tax Payable offset by reduction of AR. Operationally, Option B is significantly less disruptive.

For invoices already in open periods (May / Jun 2026), Option A direct edit is straightforward; we can use that path for those.

---

### 5. Items requiring your input

We are holding all changes pending your responses to the following:

1. **Confirm the tier classification and amounts** in the attached workbook are accurate.
2. **Tier 2 (20 fully-unpaid invoices, $334.17 tax)** – Do we remove tax now since the customer has an exemption certificate, or wait for the customer's payment to determine intent?
3. **Tier 0 (26 no-tax invoices, $3,700.99 unpaid)** – These have no tax line in NetSuite, so tax removal is not applicable. Please advise the intended action – likely a collection follow-up rather than a tax adjustment.
4. **Tier 3 (INV681804 and INV687698)** – Can the AR specialist investigate the payment application history for these two invoices before any tax change?
5. **Approach decision: Option A (direct edit with period reopen) or Option B (credit memo to current period)** for the 55 T1 invoices?
6. **Customer 1727 record update** – Please confirm who will mark `taxable = F` and attach the exemption certificate, and when.
7. **AVATAX line-level handling** – If proceeding with Option A: preference for per-line tax code change versus per-transaction AVATAX skip flag?
8. **Credit memos pending application (5 items, $140.19 credit)** – Please advise which invoices to apply these against.

---

### 6. Next steps once you respond

1. Apply your tier confirmations / reclassifications to the workbook.
2. Customer 1727 record update completed (per Q6).
3. We perform a test edit on a single Jun 2026 invoice to validate AVATAX behavior end-to-end.
4. Execute the approved approach (Option A or B) in batches, with verification after each batch.
5. Re-run the AR aging and reconcile to confirm only the intended changes posted.

We have made no changes to NetSuite to date. Everything will hold until we have your confirmation on the items above.

Please let me know if it would help to set up a quick call to walk through the workbook before you reply.

Thanks,
[Your name]
