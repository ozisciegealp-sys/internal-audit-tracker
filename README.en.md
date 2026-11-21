# Internal Audit Standardisation and Audit-Driven Training Programme

[Türkçe](README.md) | **English**

An Excel system that consolidates cross-store internal audits (peer audits by store managers) and official audits into a **single shared structure**, scores audits automatically, tracks corrective and preventive actions (CAPA / DÖF), and turns **the most recurring non-conformities into training priorities**.

> **Note:** This file is a **rebuilt version** of the structure I built and ran for a 16-store area at a coffee chain. Because the original SharePoint workbooks and schedules are no longer in my possession, the architecture was reconstructed from memory. The scoring method (severity-based penalty weights) and food-safety question distribution are drawn from an old area report I retained.
>
> Stores, checklist items, findings, dates, and actions are synthetic. Checklist descriptions are generic and not copied from the company's audit forms.

## What problem it solves

The area runs three audit types: general operations (ASA), loss prevention & partner assurance (PAP), and food safety (RSA). Before this system, results were read individually from PDF reports, making cross-store comparison, recurring-finding detection, and internal-vs-official audit benchmarking impossible.

In this system:

- **Cross-store internal audits** are scheduled quarterly: nearby store managers audit each other, each focusing on their specialty audit type. The schedule automatically flags invalid assignments (self-audit or out-of-specialty).
- **Estimated official audit dates** live in the same schedule and trigger upcoming alerts.
- Every audit and finding is logged in a **standard format**; scores compute automatically from findings.
- The **Dashboard** displays each store's internal and official scores side by side; the gap measures how well internal audits catch real issues, while providing visibility across stores.
- The **Priority List** weights recurring non-conformities by severity, linking each item to its training topic and most affected store to drive the area training programme and store-level actions.

## Before

Internal audit records had no shared structure, and official audit outcomes were reviewed one by one via PDF files.

## Sheets

| Sheet | Purpose |
|---|---|
| `Nasil_Kullanilir` | Workflow, scoring rules, abbreviations |
| `Dashboard` | Store × audit type: internal score, official score, gap, rank, findings, critical findings, open/overdue CAPAs, schedule status, and chart |
| `Oncelik_Listesi` | Top 15 recurring findings (all or single audit type), totals by training topic, and chart |
| `Madde_Magaza` | Finding item × store recurrence heatmap |
| `Denetim_Takvimi` | Quarterly internal audit rotation, status, validation checks, and estimated official audit dates |
| `Denetimler` | One row per audit: date, store, audit type, internal/official, auditor, finding counts, score, target status |
| `Bulgular` | One row per non-conformity: audit ID, item code, note (item metadata auto-populates) |
| `DOF_Takip` | CAPA tracking: action, owner, due date, closure date, status, and overdue days |
| `Madde_Listesi` | Master checklist: audit type, code, text, category, severity, and mapped training topic |
| `Magazalar` | Store list, proximity cluster, and manager audit specialty |
| `Ayarlar` | Reference date, penalty weights, total questions & target scores per audit type, alert window |

## Calculations

- **Penalty points** = critical × 2 + major × 1.5 + minor × 1
- **Audit score** = (total questions − penalty points) ÷ total questions × 100
- **Target scores**: ASA 90, PAP 85, RSA 90
- **Internal − official gap**: a large positive gap signals that the internal audit missed issues caught in the official audit
- **Weighted priority score** = finding frequency × severity weight
- **CAPA status**: *Kapandı* (Closed on time), *Geç kapandı* (Closed late), *Gecikmiş* (Overdue), or *Açık* (Open)
- **Schedule status**: *Yapıldı* (Completed), *Gecikti* (Overdue), or *Yaklaşıyor* (Due within 30 days)

## Usage

No macros or setup required. `ic-denetim-sistemi.xlsx` opens in Excel 2010+ and LibreOffice.

1. At the start of each quarter, enter the rotation and estimated official audit dates on `Denetim_Takvimi` (ensure zero red validation flags).
2. Log each completed audit on `Denetimler` and fill in the actual date on `Denetim_Takvimi`.
3. Log every finding on `Bulgular` (audit ID, item code from dropdown, note).
4. Record required corrective actions on `DOF_Takip` and enter closure dates upon completion.
5. Update **Bugünün tarihi** on `Ayarlar` (or set `=TODAY()`).
6. Use `Dashboard`, `Oncelik_Listesi`, and `Madde_Magaza` for reviews and training planning.

## Adapting to your data

| Location | What to adjust |
|---|---|
| `Madde_Listesi` | Your organization's audit checklist, severities, and training topics |
| `Magazalar` | Stores, proximity groups, and manager specialties |
| `Ayarlar` | Penalty weights, total question counts, and target scores |

`Bulgular` ships with formulas pre-filled for ~570 finding rows; extend down as needed. `Dashboard` and `Madde_Magaza` are sized for 8 stores and can be extended by copying rows/columns.

## Limitations

- Rotation is planned manually; the system validates rather than auto-assigns.
- Raw audit checklists are conducted outside the file; findings are logged post-audit.
- Total question counts for ASA and PAP are sample figures.

## License

MIT. See `LICENSE` for details.
