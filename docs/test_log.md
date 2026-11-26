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

# Project Progress Log

## Bronze Layer
- Created the Bronze data folder.
- Saved the raw items, loans, members and branches datasets.
- Checked that saved row counts and columns matched the original datasets.
- Preserved the original data without applying cleaning transformations.

## Silver Layer – Items
- Converted replacement costs from currency-formatted text to numeric values.
- Identified 24 missing replacement costs and retained them as missing.
- Validated replacement costs against expected ranges for each item type: 0 out-of-range values.
- Compared item classifications with the reference mapping: 0 mismatches.
- Standardised classifications into 8 consistent groups.
- Checked for duplicate item IDs: 0 duplicates.
- Confirmed the Silver dataset contains 1,200 rows and 8 columns.
- Saved and verified `data/silver/silver_items.csv`.

## Next Steps
- Commit the Silver items work and CSV to GitHub.
- Continue Silver-layer cleaning and validation for loans, members and branches.
- Record validation results and any data-quality issues in the project log.
