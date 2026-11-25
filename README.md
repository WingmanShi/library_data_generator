# Community Library Data Pipeline

## Project Overview

This project develops an analytics engineering data pipeline using a fictional community library dataset covering the year 2025.

The project aims to transform raw library data into clean, reliable and business-ready datasets for analysis and visualisation.

## Project Architecture

The pipeline follows a three-layer architecture:

### Bronze Layer
- Ingest original source files.
- Preserve raw data.
- Record data ingestion information.

### Silver Layer
- Clean and standardise data.
- Handle missing and inconsistent values.
- Resolve classification mapping issues.
- Validate loan periods and fine calculations.
- Remove duplicates where appropriate.

### Gold Layer
- Create business-ready datasets.
- Prepare analytical tables.
- Support Tableau visualisations.

## Current Progress

- [x] Initial data inspection
- [x] Data profiling
- [x] Postcode quality checks
- [x] Loan period validation
- [x] Fine validation
- [ ] Resolve classification mapping issues
- [ ] Investigate fine mismatches
- [ ] Implement Bronze layer
- [ ] Implement Silver layer
- [ ] Implement Gold layer
- [ ] Develop Tableau dashboard
- [ ] Complete documentation and testing

## Tools and Technologies

- Python
- Pandas
- Google Colab
- GitHub
- Tableau

## Repository Structure

```text
library_data_generator/
│
├── library_data_generator.ipynb
├── README.md
├── docs/
│   └── test_log.md
├── data/
│   ├── bronze/
│   ├── silver/
│   └── gold/
└── tests/
```

## Data Privacy

The project uses an individually generated fictional library dataset. Original data and personal identifiers should be handled carefully and should not be exposed publicly.

## Development Approach

Development is documented through incremental GitHub commits to demonstrate progress throughout the project.
