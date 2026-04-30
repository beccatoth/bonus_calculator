# Consultant Bonus Calculator

A browser-based tool for **semi-annual profitability and bonus payout analysis**. Upload three spreadsheets, set your bonus period and rates, and get project-level and employee-level results with Excel export. **All processing happens in your browser**—no server or account required.

## Features

- **Configurable bonus period** (start/end dates), **bonus payout %**, and **fringe %**
- **Three data inputs**: billable client hours, consultant submitted hours, and employee roster / salaries
- **CSV or Excel** (`.csv`, `.xlsx`, `.xlsx`) via drag-and-drop or file picker
- **Data issues panel** for rows excluded or flagged during validation
- **Results**: project summary (revenue, cost, margin, consultants) and per-employee detail, with sorting and filters
- **Download results** as Excel with formulas from the results tabs

## Quick start

### Option A — Open the file directly

Double-click `consultant_bonus_calculator.html` or open it from your browser (**File → Open**).  
Some browsers restrict local file access; if anything misbehaves, use Option B.

### Option B — Local dev server (recommended)

Requires [Node.js](https://nodejs.org/) (includes `npm`).

```bash
git clone <your-repo-url>
cd "Build After Dark 3"
npm install
npm run dev
```

Then open **http://localhost:3000/** — the dev server is configured to load the calculator at the site root (see `serve.json`).

## Data files

Upload **all three** files before running **Calculate**.

| File | Purpose | Expected columns |
|------|---------|------------------|
| **Billable client hours** | Revenue-side hours and rates | `employee_id`, `project_code`, `date`, `billed_hours`, `client_rate` |
| **Consultant submitted hours** | Submitted / worked hours | `employee_id`, `project_code`, `date`, `submitted_hours` |
| **Employee roster** | Names, salary, org structure | `employee_id`, `employee_name`, `annual_salary`, `start_date`, `end_date`, `department`, `employee_type`, `manager` |

Sample files for testing live in the repo root: `sample_billable_hours.csv`, `sample_submitted_hours.csv`, `sample_employee_roster.csv` (synthetic demo data).

## Tech stack

- Single-page **HTML/CSS/JavaScript** (no build step for the app itself)
- [SheetJS (xlsx)](https://sheetjs.com/) loaded from CDN for parsing and Excel export
- [serve](https://github.com/vercel/serve) for local preview (`npm run dev`)

## Privacy

Inputs are read in-memory in your browser. Nothing is uploaded to a backend by this project.

## Repository layout

| Path | Description |
|------|-------------|
| `consultant_bonus_calculator.html` | Main application |
| `serve.json` | Local server rewrites (root URL → calculator) |
| `vercel.json` | Same rewrites for [Vercel](https://vercel.com/) (Vercel does not read `serve.json`) |
| `package.json` | Dev dependency and `npm run dev` script |
| `sample_*.csv` | Example data |

### Deploying to Vercel

Connect the repo and deploy as a static site. Vercel’s default root is `index.html`; this project uses **`vercel.json`** so `/` and `/index.html` serve `consultant_bonus_calculator.html` without maintaining a duplicate file.

---

If you use real employee or client data, treat those exports as **confidential** and avoid committing them to a public repository.
