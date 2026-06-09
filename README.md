# Clergy Compensation Calculator

A browser-based calculator for computing United Methodist clergy compensation packages. Designed for use by District Superintendents. **In testing and not approved for official use**.

No installation required. No server required. Open `index.html` directly in any browser, or visit the hosted version at [simeonlaw.info/benefits-calculator](https://simeonlaw.info/benefits-calculator).

---

## Features

- **Two-conference support** — a single selector switches all calculations, constants, and minimum-salary logic between the New York (NY) and New England (NE) Annual Conferences
- **HealthFlex ACH billing toggle (NE only)** — indicates whether the church is billed for HealthFlex by ACH (bank draft), applying the discounted ACH rate instead of the blended rate; defaults to "yes"
- **Full compensation package calculation** — salary, accountable reimbursement (ARP), HealthFlex, Compass/UMPIP retirement, and CPP (or UMLife Options, where applicable)
- **Appointment-level aware** — benefit eligibility varies by appointment percentage (100%, 75%, 50%, 25%)
- **Multi-point charge support** — up to 15 churches with even or custom cost-share splits
- **Real-time salary minimum check** — flags salaries below the 2026 conference minimum salary schedule; soft note for retired clergy
- **Editable constants** — all year-specific rates (HealthFlex, DAC reference, salary schedule, etc.) are updatable via the Advanced Settings panel without editing code
- **Copyable output** — results table copies to clipboard with formatting preserved for pasting into Word or email
- **Export to Statement of Understanding (SOU)** — generates a downloadable .docx pre-filled with the calculated compensation figures (salary, ARP, housing allowance, HealthFlex, Compass/UMPIP, CPP, and total cost), the matching appointment-level checkbox, and the clergy/laity status code; ready for the District Superintendent to complete and route for signatures
- **Calculation detail** — toggle a plain-language explanation of how each figure was derived
- **Label toggle** — switch between abbreviated (ARP, CPP, UMPIP) and full terminology

---

## Data

Figures reflect **2026 conference recommendations**. Each conference has its own set of editable constants in Advanced Settings.

**NY (New York Annual Conference):**

| Item | 2026 Value |
|---|---|
| HealthFlex Blended Rate | $22,200 |
| ARP Full-Time Minimum | $6,400 |
| ARP Per ¼-Time Increment | $1,600 |
| MCAA (2 churches) | $1,500 |
| MCAA (3+ churches) | $3,000 |
| Compass Rate | 11% of Total Compensation |
| UMPIP Minimum Rate | 7% of Total Compensation |
| CPP Rate | 3% of Total Compensation, capped at 2× CPP cost of DAC |
| CPP DAC Reference Rate | $1,587 |

**NE (New England Annual Conference):**

| Item | 2026 Value |
|---|---|
| HealthFlex Blended Rate | $22,596 |
| HealthFlex ACH Rate | $21,468 (discounted rate for churches billed by ACH/bank draft; defaults on — reported as discontinued starting in 2027) |
| Reimbursable (ARP) Full-Time Minimum | $3,700 |
| Compass Rate | 11% of Total Compensation |
| UMPIP Recommended Rate | 10% of Total Compensation |
| CPP Rate | 3% of Total Compensation (no cap noted) |
| UMLife Options Rate | 1% of Total Compensation (CPP alternative, ¾ time and below) |

Minimum salary figures follow each conference's 2026 minimum salary schedule. NY uses a year-by-year lookup table; NE uses a base amount by clergy type plus a flat add-on by years-of-service bracket.

---

## Usage

1. Open `index.html` in a browser (Chrome, Firefox, Edge, or Safari)
2. Select a conference (NY or NE)
3. Enter pastor information, salary, ARP, and housing details
4. Add church information for multi-point charges
5. Click **Calculate**
6. Copy the results table directly into an email or Word document
7. Click **Show calculation detail** for a breakdown of how each figure is calculated. Useful for copying into an SOU for multi-point charges.

To update rates for a new year, click **⚙ Advanced Settings** at the bottom of the page and edit the constants directly — no code changes required. Each conference has its own set of editable constants.

---

## Version

**v0.12.7** — expanded the Clergy / Laity Status dropdown with all 34 UMC status codes (from the conference codes reference), sorted by category and labeled with their 2–3 letter codes in parentheses. Sorted core statuses (FE › FD › PE › PD › AM › FL) appear at the top of both conference lists; NY additionally groups PL and SL immediately after FL. NE local pastor sub-categories (M.Div./COS/Other) now show combined codes (FL/PL/SL/OL) since any of those four statuses may hold that appointment. Added STATUS_MIN_KEY mappings for all newly added statuses with salary minimums; statuses with no minimum (retired, laity, n/a) silently suppress the below-minimum warning. SOU export now auto-fills the pastor type / clergy status dropdown in both the NY ("Pastor type:") and NE ("Clergy Status/Conference Relationship") templates from the selected status, with conference-specific option mappings; NE local pastor sub-categories are left blank for the DS to specify (FL/PL/SL/OL). Fixed a typo in the NY SOU template: "Provisonal Elder" corrected to "Provisional Elder" in the Word dropdown list

**v0.12.6** — improved SOU export for both conferences: NY now fills the Pastor Name and Church/Charge Name fields; the Total Cost field is replaced with a plain-text cost breakdown (single-point: addition expression; multi-point: cost-share percentages per church followed by per-item per-church amounts), rendered at 12pt. Both NY and NE exports fill the Church/Charge Name field. Added an optional Church / Charge Name input for single-point charges (hidden when two or more churches are entered)

**v0.12.5** — added multi-point charge support to the NE SOU export: for 2-church charges, fills the per-church rows in the HealthFlex percentage-split table and the Compass/CPP per-church amount table; for 3+ churches, inserts additional rows into both tables so all churches are listed. Also fixed several NE-specific substitution bugs: dollar fields no longer double up the `$` sign (the NE template already has a literal `$` preceding each dollar field); church names and amounts now land in the correct content controls (the NE template uses different placeholder strings — `Enter text` / `Enter amount` — from the NY template, causing field values to shift into the wrong cells until the regex was corrected); and the housing field correctly shows `0` when a parsonage is provided instead of `n/a` (which produced `$n/a` in the exported document)

**v0.12.4** — fixed the underlying cause of the "exported SOU .docx won't open in Word" bug for good (it was a mismatch between the `.docx` file extension and the embedded template's internally-declared OOXML content type — Word validates this and reports a generic "we found a problem with its contents" error when they disagree; no amount of zip-byte-level correctness could fix it). Replaced the embedded template with a proper Word-resaved `.docx` (rather than the original `.dotx`) so the extension and declared content type now agree — this also avoids `.dotx`'s "always opens as a new copy" behavior, so the export now opens directly as the document itself, the right UX for a completed/ready-to-submit SOU. Also filled in several previously-blank SOU fields that weren't being transferred from the calculator: Total Service Time, "A parsonage will be provided" (Yes/No), and Housing Allowance (now shows "n/a" when a parsonage rather than an allowance is selected). Filled-in values now display bold and black instead of the template's gray placeholder styling

**v0.12.3** — fixed the actual remaining cause of "exported SOU .docx won't open in Word" (the file opened fine in LibreOffice, isolating the problem to Word's stricter zip parsing): JSZip always writes "version needed to extract = 1.0" regardless of compression method, which is internally inconsistent for DEFLATE-compressed entries (DEFLATE requires version >= 2.0 per the zip spec) — Word rejects that inconsistency outright while LibreOffice and Python's zipfile ignore the version field. Switched to STORE (uncompressed) packaging, whose version field is consistent with its method; file size returns to ~575KB but opens correctly everywhere

**v0.12.2** — fixed a second cause of the "exported SOU .docx won't open in Word" bug, specific to Firefox: the blob URL was revoked immediately after triggering the download, racing with the browser's asynchronous download read and producing a correctly-sized but corrupted file; the revocation is now delayed

**v0.12.1** — fixed a bug where the exported SOU .docx was abnormally large (~575KB instead of ~100KB) by switching from STORE to DEFLATE compression; *(superseded by v0.12.3 — DEFLATE turned out to trigger a separate JSZip zip-header inconsistency that Word rejects, so the export reverted to STORE; the size regression is an acceptable tradeoff for opening correctly in Word)*

**v0.12.0** — added an "Export to SOU (.docx)" feature: generates a Word document pre-filled from the calculation results using the conference's Statement of Understanding template (`reference/2026-SOU.dotx`), including the matching appointment-level checkbox. Generated entirely in the browser (no server) using a vendored copy of [JSZip](https://stuk.github.io/jszip/) and an embedded, tag-marked copy of the template

**v0.11.3** — removed developer/maintainer-facing instructional notes ("review this setting... when updating for that year", "remove or zero out... when updating for that year") from the user-facing HealthFlex ACH toggle and Advanced Settings panel; that guidance belongs in internal documentation, not the live tool

**v0.11.2** — fixed a bug where the below-minimum-salary warning did not appear on first page load (or right after switching conferences), even though the salary field is pre-formatted to "$0", which is below every minimum

**v0.11.1** — fixed a bug where an explicitly entered salary of $0 was not flagged as below the minimum salary (the check was incorrectly skipped for any falsy/zero value, not just an empty field)

**v0.11.0** — added a HealthFlex ACH billing toggle for the NE conference (discounted rate for churches billed by ACH/bank draft, defaults to on; reported as discontinued starting in 2027)

**v0.10.0** — added New England Annual Conference (NE) support alongside New York (NY); single conference selector switches all calculations

---

## Credits

Designed by **Simeon Law**  
Calculator built with Claude Sonnet 4.6 (Anthropic)  
Banner image created with ChatGPT GPT-5.5 (OpenAI)  
SOU export feature uses a vendored copy of [JSZip](https://stuk.github.io/jszip/) v3.10.1 (dual MIT/GPLv3-licensed)
