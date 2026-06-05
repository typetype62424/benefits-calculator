# Clergy Compensation Calculator

A browser-based calculator for computing United Methodist clergy compensation packages. Designed for use by District Superintendents. **In testing and not approved for official use**.

No installation required. No server required. Open `index.html` directly in any browser, or visit the hosted version at [simeonlaw.info/benefits-calculator](https://simeonlaw.info/benefits-calculator).

---

## Features

- **Full compensation package calculation** — salary, accountable reimbursement (ARP), HealthFlex, Compass/UMPIP retirement, and CPP
- **Appointment-level aware** — benefit eligibility varies by appointment percentage (100%, 75%, 50%, 25%)
- **Multi-point charge support** — up to 15 churches with even or custom cost-share splits
- **Real-time salary minimum check** — flags salaries below the 2026 conference minimum salary schedule; soft note for retired clergy
- **Editable constants** — all year-specific rates (HealthFlex, DAC reference, salary schedule, etc.) are updatable via the Advanced Settings panel without editing code
- **Copyable output** — results table copies to clipboard with formatting preserved for pasting into Word or email
- **Calculation detail** — toggle a plain-language explanation of how each figure was derived
- **Label toggle** — switch between abbreviated (ARP, CPP, UMPIP) and full terminology

---

## Data

Figures reflect **2026 conference recommendations** as adopted by the Commission on Equitable Compensation:

| Item | 2026 Value |
|---|---|
| HealthFlex Uniform Rate | $22,200 |
| ARP Full-Time Minimum | $6,400 |
| ARP Per ¼-Time Increment | $1,600 |
| MCAA (2 churches) | $1,500 |
| MCAA (3+ churches) | $3,000 |
| Compass Rate | 11% of Total Compensation |
| UMPIP Minimum Rate | 7% of Total Compensation |
| CPP Rate | 3% of Total Compensation |
| CPP DAC Reference Rate | $1,587 |

Minimum salary figures follow the 2026 Minimum Salary Schedule (3% increase across all categories).

---

## Usage

1. Open `index.html` in a browser (Chrome, Firefox, Edge, or Safari)
2. Enter pastor information, salary, ARP, and housing details
3. Add church information for multi-point charges
4. Click **Calculate**
5. Copy the results table directly into an email or Word document
6. Click **Show calculation detail** for a breakdown of how each figure is calculated. Useful for copying into an SOU for multi-point charges.

To update rates for a new year, click **⚙ Advanced Settings** at the bottom of the page and edit the constants directly — no code changes required.

---

## Version

**v0.9.4.1** — 2026 data

---

## Credits

Designed by **Simeon Law**  
Calculator built with Claude Sonnet 4.6 (Anthropic)  
Banner image created with ChatGPT GPT-5.5 (OpenAI)
