# Wealthy - Bug & Gap Tracker

Found by a multi-agent audit on 2026-07-06, each finding verified against `index.html`.
Ranked by (daily-use impact) x (effort). Effort: **S** small, **M** medium, **L** large.

## 🔴 High - wrong daily numbers or data loss
- [x] 1. (S) Skipping a fixed expense still reserves it in the flexible budget → "remaining" shows too low.
- [ ] 2. (M) Fixed expenses only generate for the month you open; skipped months stay empty forever → balances too high.
- [x] 3. (S) Amounts render rounded to whole shekels while data keeps agorot → rows don't sum to the total.
- [x] 4. (S) Month-end installment purchases produce impossible dates (2026-02-31) → editing breaks the date.
- [x] 5. (M) Two-device sync is blind last-writer-wins → concurrent edits silently clobbered.
- [x] 6. (M) Logging in from local-only mode discards unsynced local transactions.
- [x] 7. (S) Backup restore wipes everything instantly with no confirmation.

## 🟡 Medium
- [x] 8. (S) SMS card matching uses substring compare → charge routed to the wrong account.
- [ ] 9. (M) Editing one installment doesn't rebalance the group → rows no longer sum to the total.
- [x] 10. (S) Edit sheet allows saving amount 0 (Add blocks it); a 0 then breaks the category bar (NaN width).
- [ ] 11. (M) Deleting a fixed rule orphans the current month's generated charge.
- [ ] 12. (M) No recurring income → salary re-entered manually every month.
- [ ] 13. (M) No end date for a fixed expense → canceled subs keep generating charges.
- [ ] 14. (S) No text search / filter of transactions.
- [ ] 15. (M) No refund / credit / negative-amount support.
- [ ] 16. (M) SMS parser supports only the standard Isracard format.

## ⚪ Low - edit gaps, visibility, cosmetic, accessibility
- [ ] 17. (S) Transfer destination account can't be edited (only delete + re-add).
- [ ] 18. (M) No visibility into upcoming installment load.
- [ ] 19. (S) Expense rows show no minus sign (color is the only cue).
- [ ] 20. (S) Negative sign uses Hebrew Maqaf (U+05BE), not a real minus.
- [ ] 21. (S) Fixed-expense list shows the chosen day even when generation clamps it to the 28th.
- [ ] 22. (S) Failed localStorage write is ignored by persist → local saves silently lost.
- [ ] 23. (S) Transaction meta line has no truncation → awkward wrap on narrow phones.
- [ ] 24. (S) Transfers are invisible in every breakdown and monthly total.
- [ ] 25. (M) No multi-currency support for foreign charges.
- [ ] 26. (S) migrate() stamps schemaVersion unconditionally → masks future breaking migrations.

---

## Progress
- **Batch 1** ✅ merged: #1, #3, #4, #7, #8, #10 (small, high-impact correctness + safety).
- **Batch 2** ✅ merged: #5, #6 (sync safety - merge-by-id so no device clobbers another).
- **Next up** - the recurring-expense holes: #2, #11, #12, #13.
