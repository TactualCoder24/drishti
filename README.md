# Drishti Control Room

An interactive planning dashboard for **Project Drishti**, a three-year, ₹150 Cr supply chain programme at ACPL. ACPL has stock-outs and excess stock at the same time (fill-rate fell from 94% to 86% while inventory days rose from 39 to 46). This control room shows why, sets service targets, tests the investment plan and gives each team one place to work every week.

The whole app is a single file, [`index.html`](index.html). There is no build step, no backend and no dependencies.

## Run it

Open `index.html` in any modern browser. It also works from any static host (GitHub Pages, Netlify, an S3 bucket).

The page loads its fonts (Archivo, Public Sans, IBM Plex Mono) from Google Fonts. Without a connection it falls back to system fonts and everything else still works.

## What is in it

The app is built like a small ERP: a landing page that works as a home screen, and a dashboard with a header, section tabs and a step bar.

**Input or dashboard?** Every page is one of three kinds, and says so in a label at the top of the page and in the step bar:

| Label | Meaning | Pages |
|---|---|---|
| **Input** | You type or change data here | Service targets, New ways of working, Budget, Returns and risk, Timeline and gates (actuals), Weekly team inputs, Orders to plants, Team chat and actions, Risk register, Gate approvals |
| **Dashboard** | Read-only; calculated from what teams entered | Manager dashboard, Early warnings, Scenarios, What is going wrong, and the live summary panel on the right |
| **Guide** | A map, nothing to type | Process flow |

The landing page repeats this in a **How it works** block with a link to every screen.

**Landing page.** Pick your team (Sales, Distributors, Plants, Brands, Finance, Audit and Board, Flow Owner) and go straight to the screen you use. It also shows what **needs attention** right now (missed gates, a budget over a tranche limit, teams that have not sent this week's numbers, late order requests, open actions), a tickable **launch checklist** and the live plan numbers. **Open dashboard** opens the Manager dashboard; the DRISHTI logo takes you back to the landing page.

**Dashboard.** The header has six tabs: **Plan** (a six-step flow), **Weekly run** (three steps), **Control tower** (three steps), **Manager dashboard**, **Scenarios** and **Process flow**. It also has a **Viewing as** team switcher and a notification bell that lists the same warnings.

**Control tower** is about acting early rather than reacting late:

- **Early warnings** are raised from the plan and the weekly data before they hurt: a gate that is missed or has little headroom, spend over a tranche, a stop-loss condition, a plant over capacity, a region only partly covered, late requests, overdue actions, teams that have not sent numbers, high open risks, and gate figures waiting for sign-off. Each says why it was raised and what to do. **Make it an action** assigns it to a team and day, and posts a note in the council channel.
- **Risk register** logs risks with an owner, likelihood, impact and status. The risks already named in the plan can be loaded in one click. High risks that are still open raise a warning.
- **Gate approvals** run each funding gate through Finance (certifies), Audit and Board (verify, or send back with a note) and the Board (release or delay the tranche). A tranche can only be released if the submitted figures pass. Every step is recorded with who and when.

**Scenarios** compares five ways to run the programme side by side (Recommended plan, Board's uniform 95%, Stress case, Benefits 6 months late, Add snacks capacity): fill, days, cost of service, return, payback, value, gates, budget fit and a verdict (Proceed, Proceed with a re-test, Over budget, Do not proceed). **Use this** loads a scenario into the whole app. Below it, a phase plan (months 0–9, 10–22, 23–36) shows what to do and when, the gate tests, and what happens if a gate is missed.

- **Try a scenario** chips load the first three scenarios. **Reset** clears everything.
- A **live summary panel** on the right shows fill, days, return, payback, spend, both gates and the budget limits, plus notifications and a systems strip (WMS, ERP, DMS, Sales DB). The system status is a display-only demo; nothing is actually connected.
- **Who can do what.** On Orders to plants, Plants and the Flow Owner can commit and move orders; other teams can raise and discuss requests. A banner says which role you are viewing as.
- **Manager dashboard** summarises the weekly run: requests by stage, cannot-fill rate against the plan limit, orders waiting for a decision, **team accountability** (per team: numbers sent, requests raised, order moves, actions done and overdue, messages), the top warnings, the latest activity, the funding gates and which teams have sent their numbers.
- **Process flow** is a clickable flowchart of a week, from the numbers each team enters, through early warnings and the council, to the gate approval and tranche release.
- Detail-heavy desks keep secondary tables under **More detail** so the first screen stays short.

The six Plan desks share one model, so a change on one desk updates the others and the landing page.

| Desk | What it does |
|---|---|
| What is going wrong | Excess and shortfall by region and the root-cause tree; competing explanations and pilot reliability sit under More evidence |
| Service targets | Set fill-rate per product segment (A to E); see cost and payback against the Board's uniform 95% |
| New ways of working | The weekly rhythm, honest allocation when stock is short, and who gets paid for what |
| Budget | Move the ₹150 Cr between initiatives; tranche limits are checked as you type |
| Returns and risk | Stress recovery, delays and overruns; IRR, payback and NPV recalculate |
| Timeline and gates | 36-month roadmap, Gate 1 and Gate 2 checked against planned or actual figures |
| Weekly team inputs | Sales, distributors, plants, brands and finance enter one set of numbers per week |
| Orders to plants | Regions raise requests; plants commit a quantity and ship week on a six-column board |
| Team chat and actions | One channel per hand-off, plus the action list for Tuesday's Flow Council |

## Where your data lives

Everything is stored in your browser's `localStorage`, so nothing leaves your device and each browser keeps its own copy.

| Key | Holds |
|---|---|
| `drishti-v2` | Planning state: targets, budget, assumptions, gate actuals, launch checklist, last desk |
| `drishti-ws-v1` | Workspace: weekly inputs, order requests, messages, actions, risks, gate approvals |
| `drishti-uid`, `drishti-team` | Your local identity and chosen team |

The workspace (weekly inputs, orders, chat, and so the manager dashboard) is not shared between people or devices. If browser storage is blocked, it works for the current session only.

- **Reset to base case** clears the planning desks. It does not touch workspace entries.
- **Clear examples** (Weekly team inputs) removes everything loaded by **Load example week**.
- To wipe everything, clear this site's data in your browser settings.

## Model notes

The returns model uses monthly cash flows over 60 months, values working capital at 11% a year, certifies benefits one quarter after delivery and treats pilot costs as sunk. The base case gives an IRR of 86.6% and payback of 29.3 months. Figures are model estimates; use the Returns and risk desk to test them.

## Phones and tablets

The layout adapts below 1100 px and again below 820 px, where the header stacks, the tabs form a two-by-two grid, the step bar scrolls sideways and stays pinned, and the live summary moves below the page content. On phones, form fields use 16 px text (so iOS does not zoom on focus), touch targets are 40 to 44 px, the order board swipes sideways, and chart tooltips respond to touch.
