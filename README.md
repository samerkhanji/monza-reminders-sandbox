# Monza Installment Reminders — Sandbox

A single-file, zero-dependency local tester for the Monza installment reminder engine
(the `200_installment_reminders.sql` migration in the main
[MONZA-SAL-APP](https://github.com/samerkhanji/MONZA-SAL-APP) repo).

It's a faithful JS port of the SQL logic — rule matching, phone normalization, pilot-mode
gating, and monthly-checklist population — so you can try different dates/customers/rules
and see exactly what would fire, without touching Supabase or the real app.

## How to use it

1. Open `index.html` directly in any browser (double-click it, or drag it into a tab). No
   server, no build step, no install.
2. Load data one of two ways:
   - **Google Sheet** — paste a Sheet ID + tab (gid), click **Load from Sheet**. The Sheet
     must be shared as **Anyone with the link → Viewer** (Share → General access) or the
     fetch will fail (Google will redirect to a sign-in page instead of returning CSV).
   - **CSV upload** — click **Choose File** and pick a CSV with the same columns as
     [`supabase/tests/installment-reminders-sample-data.csv`](https://github.com/samerkhanji/MONZA-SAL-APP/blob/main/supabase/tests/installment-reminders-sample-data.csv)
     in the main repo. Use this if the Sheet isn't public yet.
3. Set "Today" for the simulated run, pilot mode, and the approved auto-send numbers.
4. Click **Run simulation** to see what would fire today, the monthly checklist, and
   anything excluded (with the reason).

The phone-normalization unit tests run automatically on every simulation — expand
"Unit tests" to see all 9 pass/fail.

## Relationship to the real app

This is a throwaway sandbox for iterating on reminder logic before it goes back into
`200_installment_reminders.sql` (SQL) and the harness at
`supabase/tests/installment-reminders-harness.mjs` (Node) in the main repo. If you change
a rule here and like the result, port the same change into both of those, not just here —
this sandbox never touches production.
