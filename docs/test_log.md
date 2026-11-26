# Data Quality Testing Log

## 1. Initial Data Inspection

Initial inspection was performed to understand the structure, content and quality of the generated library dataset.

## 2. Postcode Quality Validation

- Missing postcodes: 34
- Leading/trailing spaces: 0
- Lowercase characters: 128
- Incorrect spacing: 82
- Valid postcode patterns: 798
- Invalid postcode patterns: 0

**Action:** Standardisation of postcode formatting will be addressed in the Silver layer.

## 3. Loan Period Validation

- Incorrect loan periods: 0
- Expected loan periods were compared against actual loan periods.

**Result:** No incorrect loan periods were identified.

## 4. Classification Mapping Validation

- Unmapped classification values: 25

**Action:** Further investigation required to identify and resolve unmapped values.

## 5. Fine Validation

- Returned loans checked: 5,713
- Fine mismatches: 9
- Missing positive fines: 0
- Missing zero fines: 517
- Fines greater than £10: 3
- Negative fines: 6

**Action:** Investigate incorrect fine values and determine the appropriate treatment of missing zero-fine records.

## 6. Outstanding Actions

- [ ] Investigate classification mapping failures.
- [ ] Investigate negative fine values.
- [ ] Investigate unusually high fine values.
- [ ] Review missing zero-fine records.
- [ ] Repeat validation after corrections.
- [ ] Record final validation results.

## 7. Development Notes

The initial validation was performed for inspection purposes. The original source data was not modified during these checks.

Further transformations and corrections will be documented as development progresses.

### Referential integrity – loan item references

**Status: Identified – intentional data-quality issue**

**Initial findings:**
- Original items table contains 1,200 unique item IDs (`I0001`–`I1200`).
- Mapping table contains the same 1,200 item IDs.
- No duplicate item IDs were found in the mapping table.
- Original loan data contains 25 distinct item IDs that do not exist in the items table.
- These invalid references occur in 30 loan records.

**Root cause:**

Inspection of the supplied `generate_library_data_by_id.py` generator identified an intentional data-quality injection in the loan-generation section. The generator replaces 0.5% of loan item references with randomly generated IDs between `I1201` and `I1299`.

**Conclusion:**

The 30 affected loan records represent an intentional referential integrity issue in the supplied dataset, rather than an error in the mapping table or the student's data preparation.

**Planned treatment:**

Preserve the original Bronze data. Identify unmatched item references during Silver transformation and flag or quarantine affected records so they are not incorrectly included in downstream Gold reporting. Document the treatment and its impact on record counts.

### Bronze Layer — Raw Data Ingestion

The Bronze layer was created to preserve the original source datasets before any cleaning or transformation.

The following datasets were saved as CSV files in `data/bronze/`:

| Dataset | Records |
|---|---:|
| Items | 1,200 |
| Loans | 6,060 |
| Members | 832 |
| Branches | 8 |

**Validation performed:**
- Confirmed that all four CSV files were successfully created.
- Compared the original and Bronze record counts.
- Checked that the original and Bronze column names match.

All four datasets passed these checks.

No cleaning or corrections were applied during Bronze ingestion. Data quality issues identified during inspection will be investigated and handled in the Silver layer.
