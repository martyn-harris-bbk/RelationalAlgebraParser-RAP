# RelationalAlgebraParser (RAP)

Prototype markdown‑to‑relational‑algebra converter – ideal for quickly dropping nicely formatted algebra into Word docs, PowerPoint slides, wikis, or anywhere that supports basic HTML.

## Introduction
RAP takes *plain‑keyword “markdown”* such as

```text
PROJECT(name)(SUPPLIER) PERSONNEL UNION ALUMNI
```
... and turns it into textbook symbols:

```text
π₍name₎(SUPPLIER) PERSONNEL ∪ ALUMNI
```

It currently supports the eight core operators plus `RENAME`:

| Keyword | Symbol |
|---|---|
| `UNION` | ∪ |
| `INTERSECTION` | ∩ |
| `DIFFERENCE` / `MINUS` | – |
| `PRODUCT` | × |
| `JOIN` | ⋈ |
| `DIVIDE` | ÷ |
| `SELECT(condition)` | σ<sub>condition</sub> |
| `PROJECT(attrs)` | π<sub>attrs</sub> |
| `RENAME(map)` | ρ<sub>map</sub> |

> **Disclaimer** — RAP is a proof‑of‑concept. No warranty of correctness or fitness for purpose is provided. Always check the resulting output before using it for tutorials or assessmments.

##  Running the app
1. **Download** `relational_algebra_editor.html` (the single‑file app).
2. **Open** it in any modern browser (Chrome, Edge, Firefox, Safari).
3. **Type** or paste markdown in the left pane.
4. **Copy** the rendered algebra with the **Copy** button.
5. **Paste** into Word, PowerPoint, Notion, etc. – subscripts are preserved because the output is just HTML.

> Tip: Word & PowerPoint keep the subscript formatting intact when you paste – no extra tweaking needed.

---

## Example walk‑through

| # | Markdown | Algebra |
|---|---|---|
| 1 | `PERSONNEL UNION ALUMNI` | `PERSONNEL ∪ ALUMNI` |
| 2 | `COURSES DIFFERENCE FULLY_BOOKED` | `COURSES – FULLY_BOOKED` |
| 3 | `PROJECT(name)(SUPPLIER)` | `π<sub>name</sub>(SUPPLIER)` |
| 4 | `SELECT(order_date ≥ '2025-01-01' AND order_date < '2026-01-01')(ORDERS)` | `σ<sub>order_date ≥ 2025‑01‑01 ∧ order_date < 2026‑01‑01</sub>(ORDERS)` |
| 5 | `RENAME(supplier_id->owner_id)(SUPPLIER)` | `ρ<sub>supplier_id→owner_id</sub>(SUPPLIER)` |

<details>
<summary>Intermediate & complex queries</summary>

```text
PRODUCT JOIN INVENTORY
⇒ PRODUCT ⋈ INVENTORY

(TRAINED_FORKLIFT INTERSECTION AVAILABLE_TODAY)
⇒ TRAINED_FORKLIFT ∩ AVAILABLE_TODAY

STUDENT PRODUCT ELECTIVE
⇒ STUDENT × ELECTIVE

PROJECT(title)(
  SELECT(price < 20 AND warehouse_region = 'UK')(
    BOOK JOIN SUPPLIER JOIN WAREHOUSE))
⇒ π<sub>title</sub>(σ<sub>price < 20 ∧ warehouse_region = 'UK'</sub>(BOOK ⋈ SUPPLIER ⋈ WAREHOUSE))

COMPLETED DIVIDE CORE_MODULE
⇒ COMPLETED ÷ CORE_MODULE
```

</details>

Pull requests and feedback welcome – just remember this is an experiment.

Credit: Martyn Harris, Birkbeck University.
