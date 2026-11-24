# Internal Audit Standardisation and Audit-Driven Training Programme

[Türkçe](README.md) | **English**

An Excel system that consolidates cross-store internal audits (peer audits by store managers) and official audits into a **single shared structure**, scores audits automatically, tracks corrective and preventive actions (CAPA / DÖF), and turns **the most recurring non-conformities into area training priorities**.

> **Confidentiality & Synthetic Data Note:** This workbook is a **rebuilt version** of the internal audit and CAPA system I built and ran across a 16-store retail area. All brand names, store identifiers, proprietary audit forms, and real findings have been omitted; all stores (`Mağaza A`–`Mağaza H`), checklist items, dates, and actions are synthetic.

## What problem it solves

Multi-store operations run three distinct audit disciplines: general operations (`ASA`), loss prevention & partner assurance (`PAP`), and food safety (`RSA`). Before this system, outcomes stayed in individual PDF reports, making cross-store comparison, root-cause recurrence analysis, and internal-vs-official score calibration impossible.

In this system:

- **Cross-store internal audits** are scheduled quarterly: nearby store managers audit each other by audit specialty, with automatic validation for invalid assignments (self-audit or out-of-specialty).
- **Estimated official audit dates** are tracked in the same schedule with upcoming-due alerts.
- Every audit and finding is logged in a **standard format**; penalty-weighted scores compute automatically.
- The **Dashboard** displays internal and official scores side by side per store, measuring how accurately peer audits reflect field reality.
- The **Priority List** weights recurring non-conformities by severity and maps each item to its training topic to drive the area quality training programme.

## Before

Internal audit records had no shared data structure, and official audit outcomes were tracked individually across separate PDF files.

## Sheets

| Sheet | Purpose |
|---|---|
| `Nasil_Kullanilir` | Workflow, scoring rules, and abbreviations |
| `Dashboard` | Store × audit type: internal score, official score, gap, rank, findings, critical findings, open/overdue CAPAs, schedule summary, and chart |
| `Oncelik_Listesi` | Top 15 recurring findings (all or single audit type), breakdown by training topic, and chart |
| `Madde_Magaza` | Checklist item × store recurrence heatmap |
| `Denetim_Takvimi` | Quarterly peer-audit rotation, validation checks, and estimated official audit dates |
| `Denetimler` | Audit log: date, store, audit type, internal/official, auditor, finding counts, and calculated score |
| `Bulgular` | Finding log: entering audit ID and item code auto-populates category, severity, and training topic |
| `DOF_Takip` | CAPA tracker: action, owner, due date, closure date, status, and overdue days |
| `Madde_Listesi` | Master checklist items, severities, and mapped training topics |
| `Magazalar` | Store list, proximity cluster, and manager audit specialty |
| `Ayarlar` | Reference date, penalty weights, total question counts, and target scores |

## Calculations

- **Penalty points** = critical × 2 + major × 1.5 + minor × 1
- **Audit score** = `(total questions − penalty points) ÷ total questions × 100`
- **Target scores**: ASA 90 · PAP 85 · RSA 90
- **Internal − official gap**: a large positive gap signals that peer audits missed issues caught in official audits
- **Weighted priority score** = finding frequency × severity weight
- **CAPA status**: *Kapandı* (Closed on time), *Geç kapandı* (Closed late), *Gecikmiş* (Overdue), or *Açık* (Open)

## Usage

Macro-free; `ic-denetim-sistemi.xlsx` opens directly in Excel 2010+ and LibreOffice.

## License

MIT. See `LICENSE` for details.
