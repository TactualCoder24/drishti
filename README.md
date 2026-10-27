# Drishti Control Room

An interactive planning dashboard for **Project Drishti**, a three-year, ₹150 Cr supply chain programme at ACPL. ACPL has stock-outs and excess stock at the same time (fill-rate fell from 94% to 86% while inventory days rose from 39 to 46). This control room shows why, sets service targets, tests the investment plan and gives each team one place to work every week.

The whole app is a single file, [`index.html`](index.html). There is no build step, no backend and no dependencies.

## Run it

Open `index.html` in any modern browser. It also works from any static host (GitHub Pages, Netlify, an S3 bucket).

The page loads its fonts (Archivo, Public Sans, IBM Plex Mono) from Google Fonts. Without a connection it falls back to system fonts and everything else still works.

## What is in it

The app opens on a **landing page** with the overview: the headline plan numbers, five key facts, a live snapshot (cash curve, funding gates, decisions needed today) and a card for each desk. **Open dashboard** takes you into the dashboard, which has a sidebar of nine desks; **← Landing page** (or the DRISHTI logo) takes you back. Opening the landing page again and pressing **Open dashboard** returns you to the desk you were last on.

The first six desks share one model, so a change on one desk updates the others and the landing page.

| Desk | What it does |
|---|---|
| What is going wrong | Excess and shortfall by region, the root-cause tree, competing explanations and how far to trust each pilot |
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
| `drishti-v2` | Planning state: targets, budget, assumptions, gate actuals, current desk |
| `drishti-ws-v1` | Workspace: weekly inputs, order requests, messages, actions |
| `drishti-uid`, `drishti-team` | Your local identity and chosen team |

The workspace (the last three desks) is not shared between people or devices. If browser storage is blocked, it works for the current session only.

- **Reset to base case** clears the planning desks. It does not touch workspace entries.
- **Clear examples** (Weekly team inputs) removes everything loaded by **Load example week**.
- To wipe everything, clear this site's data in your browser settings.

## Model notes

The returns model uses monthly cash flows over 60 months, values working capital at 11% a year, certifies benefits one quarter after delivery and treats pilot costs as sunk. It is calibrated to the submitted deck (base case IRR 86.6%, payback 29.3 months), so figures are model estimates and may differ slightly from it.

## Phones and tablets

The layout adapts below 1100 px and again below 820 px, where the side index becomes a scrolling tab strip. On phones, form fields use 16 px text (so iOS does not zoom on focus), touch targets are 40 to 44 px, the order board swipes sideways, and chart tooltips respond to touch.
