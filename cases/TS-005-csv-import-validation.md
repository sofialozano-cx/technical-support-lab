# TS-005 — CSV Import Validation Failure

## Scenario

A fictional customer reports that a customer-data CSV file uploads successfully but the import fails during validation.

**Category:** Data Import / Validation  
**Priority:** P3  
**Scope:** One customer import

---

## Customer Report

> Our CSV looks normal, but the system says some rows are invalid. We have more than 2,000 records and can't tell what's wrong.

---

## Investigation Approach

I would avoid manually reviewing thousands of rows first. Instead:

1. Obtain the exact validation message/export.
2. Confirm required columns and accepted formats.
3. Identify whether failures share a pattern.
4. Test a small sanitized sample.
5. Separate structural CSV issues from field-level validation issues.

---

## Simulated Validation Results

```text
Row 118: invalid email format
Row 604: required field "email" is empty
Row 981: invalid date format; expected YYYY-MM-DD
Row 1440: duplicate external_id "C-10392"
```

The file itself parses correctly; specific records violate field rules.

---

## Root Cause

**The import file is structurally valid CSV, but several rows fail application-level validation rules.**

---

## Resolution

- Correct invalid email values.
- Populate or intentionally exclude records missing required fields.
- Convert dates to the documented `YYYY-MM-DD` format.
- Resolve duplicate external identifiers.
- Re-run validation on a small sample before importing the complete dataset.
- Keep a backup of the source file before bulk edits.

---

## Customer-Facing Response

Hi there,

The CSV file itself is being read correctly. The import is stopping because a small number of records don't meet the field-validation rules.

The errors include an invalid email, a missing required email value, a date in the wrong format, and a duplicate external ID. I recommend correcting those rows and testing a small sample before re-running the full import.

This should let you fix the affected records without rebuilding the entire file.

Best,  
Sofia

---

## Key Learning

“CSV import failed” can describe different layers of failure: **file parsing, schema/column mapping, field validation, duplicate constraints, or processing errors**. Identifying the failing layer makes troubleshooting faster.

## Skills Demonstrated

`Data Validation` · `CSV` · `Structured Troubleshooting` · `Error Analysis` · `Customer Communication`
