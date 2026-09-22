# TMS — Transaction Maintenance System (UI Showcase)

A functional, responsive front-end prototype of a bank back-office console for consolidating daily transaction data across channels, monitoring nightly ingestion jobs, and releasing reports under maker-checker control.

Built as the UI design companion to a Business Analyst / QC case study for a **New Cash Control System**.

**🔗 Live demo:** `https://boyvalentyas-stack.github.io/tms-ui-showcase/` *(update once GitHub Pages is enabled)*

---

## Overview

This is a single self-contained HTML/CSS/JS file — no build step, no dependencies, no backend. It simulates a role-based banking console with in-memory sample data, so filters, approvals, and job re-runs actually do something rather than just looking clickable.

It covers four of the system's core screens plus login:

| Screen | Who sees it | What it demonstrates |
|---|---|---|
| **Login** | Everyone | Role selector (IT Admin / Maker / Approver) that drives everything downstream |
| **Job Monitoring Dashboard** | IT Admin | Per-source ingestion status, control totals, a working "Re-run" action for a failed source |
| **Transaction Inquiry** | All roles | Live filtering by channel/type/amount; account numbers masked unless signed in as Approver |
| **Report & Approval** | Maker, Approver | Reconciliation check before submission, maker-checker approve/reject workflow |
| **User & Role Management** | IT Admin | Add / activate / deactivate users |

## Features

- **Role-based access** — navigation items, screens, and data visibility change based on the signed-in role, mirroring the RBAC requirement in the FSD.
- **Working filters** — the Transaction Inquiry screen filters a sample dataset client-side by channel, type, and amount range.
- **Data masking** — account numbers are masked for all roles except Approver, reflecting the PDP-law-driven confidentiality requirement.
- **Reconciliation gate** — generating a Regulator report while a source (RTGS) is still missing is blocked with a variance shown, matching the control-total requirement; re-running that source in the Dashboard clears the block.
- **Maker-checker workflow** — reports move from *Pending* → *Released* only through an Approver action; rejection requires a reason.
- **Fully responsive** — sidebar navigation collapses into a bottom tab bar under ~820px width; tables scroll horizontally on small screens.
- **Light/dark aware** — follows the visitor's OS-level color scheme automatically.

## Tech Stack

- Plain **HTML5 / CSS3 / vanilla JavaScript** — no framework, no bundler
- [IBM Plex Sans](https://fonts.google.com/specimen/IBM+Plex+Sans) for UI text, [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono) for numeric/data fields, loaded from Google Fonts
- All state held in-memory (`state`, `SOURCES`, `TX`, `USERS` arrays) — refreshing the page resets the demo

## Running Locally

No installation required.

```bash
git clone https://github.com/<your-username>/tms-ui-showcase.git
cd tms-ui-showcase
open index.html   # or just double-click the file
```

Or serve it locally if you prefer:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Project Structure

```
tms-ui-showcase/
├── index.html   # entire app: markup, styles, and logic in one file
└── README.md
```

## Try It Out

1. Open the app and sign in as **IT Admin** → land on the **Job Monitoring Dashboard** → click **Re-run** on the RTGS row and watch it recover.
2. Sign out, sign back in as **Business User (Maker)** → go to **Report & Approval** → select *Regulator (Fixed layout)* → **Generate** (it will block if RTGS hasn't been re-run yet) → submit once matched.
3. Sign out, sign back in as **Business Approver (Checker)** → **Report & Approval** → approve the pending report → check **Transaction Inquiry**, where account numbers are now shown unmasked for this role.

## Background

This prototype accompanies a written FSD (Functional Specification Document) covering requirements gathering, business requirements, current/future process flows, and test scenarios for a bank's Transaction Maintenance System. The UI translates section 2.4.2 (UI Design) of that document into something interactive rather than static wireframes.

## Author

**Boy Valentyas Indra G**

## License

This project is a portfolio/demo piece and is free to reference or reuse for learning purposes.
