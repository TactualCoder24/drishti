# Drishti: what changed since yesterday

Covers 27 Oct 2026 (the first build, 22:04 to 22:49) and 28 Oct 2026 (the move onto the v2 financial model).

**Status right now**
- Everything from 27 Oct is on GitHub (`origin/main` is at `dc77735`).
- The 28 Oct work is committed on your machine as `d4ed510` and is **not pushed yet**.
- `Project_Drishti_Financial_Model_v2.xlsx` is in the folder but not committed. I did not edit it.

---

## 28 Oct: the app now runs on the v2 financial model

Your friend's v2 workbook is the latest. The app now uses its logic, so the numbers on screen match the workbook.

### What was done
1. **Read all 11 tabs of the workbook** (Data, Assumptions, Diagnostics, Service, Scenarios, Cashflow, Engine, Gates, Funding, Unfunded, Sensitivity) and checked the numbers.
2. **Replaced the app's simplified returns model** with a port of the workbook's Cashflow and Gates logic. With the base settings it reproduces all 16 scenarios on the Sensitivity tab (IRR, payback, NPV, spend, steady-state benefit all match to within 3e-10), and the Gate 1 and Gate 2 figures match the Gates tab.
3. **Scenarios page rebuilt as a pick-list of 18**: three plan choices plus the workbook's S2 to S16, grouped as recovery of lost sales, delivery risk, how benefits are counted, and everything at once.
   - Each scenario shows return, payback, value created, spend, both gates, the three tranche limits, what breaks, how to challenge it, and when and how to proceed.
   - Verdicts: Proceed, Proceed with conditions, Over budget, Do not proceed as is, Check the numbers first.
   - **Use this scenario in the app** loads it into every page. An all-scenarios table sits below it.
4. **Returns page**: two new controls (how working capital is counted, and the obsolescence and freight pool range). The stress-test table now shows the workbook's own results beside the live ones. Break-points quote the workbook.
5. **Gates and Budget pages**: the watch-outs now come from the model (for example "+0.7 d if the auditor restates the baseline"). The Budget KPI shows actual spend in 36 months.
6. **Small fixes**: negative money shows as "−₹57.1 Cr", IRRs of 500% and above show as ">500%", stale "five ways" wording removed, README updated.

### Numbers: before and after

| | Before (older deck) | Now (workbook v2) |
|---|---|---|
| 5-year IRR | 86.6% | 84.5% |
| Payback | 29.3 months | 28.2 months |
| NPV at 18% | ₹89 Cr | ₹79.1 Cr |
| Spend by month 36 | ₹131 Cr | ₹141 Cr (includes 10% contingency from quarter 4) |
| Gate 2 EBITDA | ₹75.7 Cr | ₹74.5 Cr |
| ACPL-owned working capital | ₹153 Cr | ₹142 Cr |

### Numbers that were too high, and what happened to them
| Item | Was | Now |
|---|---|---|
| Board's uniform 95% | IRR 142%: its extra ₹107 Cr cost of service was never counted | IRR 41%, payback 41 months, spend ₹256 Cr, over budget |
| Snacks capacity (Plants A and H) | ₹18 Cr a year | ₹12.1 Cr a year, as in the workbook; it does not fit inside ₹150 Cr |
| National replenishment extension | Overstated benefit | ₹10.1 Cr a year less ₹4.6 Cr running cost, as in the workbook |
| S11 Cash basis | IRR 4,188% | Shown as ">500%" and marked "Check the numbers first" |
| S10 Distributor stock counted | Verdict "Proceed" | Marked "Check the numbers first" (see below) |

### Points to raise with your friend (the workbook itself, not changed)
1. **S11 (Cash basis)** gives an IRR of 4,188%. ₹128 Cr of working capital is counted as cash in the first six quarters, so cash flow is positive from quarter 2 and IRR stops meaning anything. It should show "n/m".
2. **S10 (Distributor stock counted)** uses an owned-share multiplier of 10 (`Scenarios!K14`), which treats every initiative's stock as fully ACPL-owned. The exact ratio is 1,230 ÷ 865 = 1.42, which gives an IRR near 102% instead of 114%.
3. **Gate 2 inventory days passes by only 0.035 days** (37.965 against 38). That is because raw-material release was raised from 10% to 20%. At 10% it misses (38.6). The label on `Service!A36` still says 10%.
4. **Gate 2 working capital passes at ₹214 Cr on the network basis**, but that depends on valuing a day at ₹26.7 Cr, which implies annual cost of goods above revenue. On stock ACPL owns it is ₹142 Cr, and on a COGS-based day it is ₹128 Cr, both below the ₹170 Cr test.
5. **Payback has little room**: the base clears 30 months by 1.8 months. A one-month slip or delivery 3% below plan fails it, and the Audit Committee's 35% recovery case (S2) already fails at 35.7 months.

### How it was checked
- All 16 workbook scenarios compared against the workbook's own saved results: worst difference about 3e-10.
- The real page was run in headless Chrome and clicked through all 18 scenarios, plus loading a scenario and resetting: no JavaScript errors.
- Desktop and phone-width screenshots checked.

### Not done
- **Editable inputs** (your own scenario, editable limits) were started and then dropped at your request. Nothing from that is in the app.
- The workbook was not edited. The fixes above are for your friend to make.
- The 28 Oct commit is not pushed.

---

## 27 Oct: the first build (all on GitHub)

| Time | Commit | What it did |
|---|---|---|
| 22:04 | `219985d` | Team inputs, orders board and chat now store in the browser (no claude.ai-only database), so they work on any host. Mobile layout improved. README added. |
| 22:05 | `85862cf` | Page renamed to `index.html` so Vercel, GitHub Pages and Netlify serve it at the root (it was returning 404). |
| 22:09 | `2d2a22b` | Landing page added; the nine desks moved behind an "Open dashboard" button. |
| 22:20 | `e792446` | Rebuilt as an ERP-style app: top header with Plan and Weekly run tabs, "Viewing as" team switcher, notification bell, step bar, launch checklist and a "Needs attention" list on the home screen. |
| 22:30 | `f09703a` | Manager dashboard, process-flow chart, live summary panel, scenario chips (A, B, C and Reset), role-aware orders board, heavy desks simplified. |
| 22:37 | `004d959` | Every page labelled Input, Dashboard or Guide, with a tag under each step. |
| 22:49 | `dc77735` | Control tower: early warnings that can become owned actions, risk register, gate approvals (Finance, then Audit and Board, then release or delay), scenario comparison, and an Audit and Board team. |
