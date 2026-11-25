# Data Quality Testing Log

## Initial Data Inspection and Validation

### Test 1: Loan Period Validation
- **Check:** Compared actual loan periods against expected loan periods.
- **Method:** Calculated the difference between loan date and due date and compared it with the expected loan duration.
- **Result:** 0 incorrect loan periods.
- **Action:** No correction required.

### Test 2: Classification Mapping
- **Check:** Checked whether all classification values were successfully mapped.
- **Method:** Identified records with unmapped classification values.
- **Result:** 25 classification values were not successfully mapped.
- **Action:** Further investigation required.

### Test 3: Fine Validation
- **Check:** Compared calculated fines against expected fines for returned loans.
- **Method:** Compared actual numeric fines with expected fines based on late days and applicable fine rates.
- **Result:** 5,713 returned loans checked; 9 incorrect fines identified.
- **Additional findings:** 6 negative fines, 3 fines greater than £10, and 517 missing fines where zero was expected.
- **Action:** Investigate fine calculation logic, incorrect values and missing zero fines before finalising the Silver layer.
