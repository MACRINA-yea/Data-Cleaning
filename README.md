# FIFA 21 Data Cleaning

This project cleans the raw FIFA 21 player dataset (18,979 players, 77 columns), which contains several common real-world data quality issues.

## Issues Found & Fixed

1. **Club names** had stray leading whitespace/newlines (`'\n\n\n\nFC Barcelona'`) — stripped.
2. **Currency columns** (`Value`, `Wage`, `Release Clause`) were stored as text (`'€103.5M'`, `'€560K'`) — converted to numeric floats.
3. **Height/Weight** mixed metric and imperial units in the same column (`'170cm'` vs `'6'2"'`) — standardized to `Height_cm` and `Weight_kg`.
4. **Contract** mixed three formats: year ranges (`'2004 ~ 2021'`), `'Free'`, and loan end dates (`'Jun 30, 2021 On Loan'`) — split into `Contract_Start`, `Contract_End`, and `Contract_Status`.
5. **Star ratings** (`W/F`, `SM`, `IR`) were stored as text (`'4 ★'`) — converted to plain integers.
6. **Hits** used shorthand notation (`'1.6K'`) and had missing values — converted to numeric, nulls filled with 0.
7. **Loan Date End** nulls actually meant "not on loan," not missing data — converted to datetime and added an explicit `On_Loan` boolean flag.
8. **Redundant columns** (`photoUrl`, `playerUrl`, `Name`) dropped, keeping `LongName` as the single name field.
9. **Joined** date converted from text (`'Jul 1, 2004'`) to a proper datetime type.

## Tools Used

- Python
- pandas
- re (regex)

## Output

Running the cleaning notebook produces `fifa21_cleaned.csv` — a fully numeric/typed, analysis-ready version of the original dataset.

## Source Data

Original dataset: FIFA 21 player data (Kaggle).
