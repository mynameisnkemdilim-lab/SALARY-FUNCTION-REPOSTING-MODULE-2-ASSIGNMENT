# SF Employee Salary Analysis — Assignment

A Jupyter Notebook + R workflow that covers **data import, function design,
dictionary processing, error handling, CSV/ZIP export, and R-based extraction**
using San Francisco city salary data (2011–2018).

---

## Repository Structure

```
sf_salary_project/
│
├── SF_Salary_Analysis.ipynb   ← Main Jupyter Notebook (Python)
├── unzip_and_display.R        ← R script for Task 6
├── Total.csv                  ← Dataset (add your own copy here)
└── README.md                  ← This file
```

---

## Requirements

### Python
| Package | Version (min) |
|---------|--------------|
| Python  | 3.8+         |
| pandas  | 1.3+         |
| numpy   | 1.21+        |
| seaborn | 0.11+        |
| matplotlib | 3.4+      |
| jupyter | 1.0+         |

Install all at once:
```bash
pip install pandas numpy seaborn matplotlib jupyter
```

### R
| Package | Notes |
|---------|-------|
| R       | 4.0+ (base `unzip` and `read.csv` are used — no extra packages needed) |

---

## Setup & Usage

### Step 1 — Add the dataset

Place `Total.csv` (SF salary data) in the project root, **or** the notebook
will automatically generate a synthetic 320-row sample so every cell still runs.

Download the original dataset from Kaggle:  
<https://www.kaggle.com/datasets/kaggle/sf-salaries>

---

### Step 2 — Run the Jupyter Notebook

```bash
cd sf_salary_project
jupyter notebook SF_Salary_Analysis.ipynb
```

Run all cells top-to-bottom (**Kernel → Restart & Run All**).  
The notebook will:

| Task | What it does |
|------|-------------|
| 1 | Import `Total.csv` (or synthetic fallback), coerce pay columns to float |
| 2 | Define `get_employee_details(name, df)` — returns all records for that employee |
| 3 | Build `employee_dict` — a `{NAME: [records]}` lookup dictionary |
| 4 | Demonstrate 4 error-handling scenarios (valid, not found, empty string, None) |
| 5 | Export chosen employee to CSV → compress into `Employee_Profile.zip` |
| 6 | Show the R script content; instruct how to run it |

After Task 5 finishes you will see `Employee_Profile.zip` in the project root.

---

### Step 3 — Run the R Script (Task 6)

Open **RStudio** or an R terminal, set your working directory to the project
root, then:

```r
setwd("/path/to/sf_salary_project")
source("unzip_and_display.R")
```

**Or** from the command line:

```bash
Rscript unzip_and_display.R
```

The script will:
1. Validate `Employee_Profile.zip` exists  
2. Extract it to a temporary directory  
3. Discover all CSV files inside  
4. Print dimensions, column names, summary statistics, and the full table  

---

## Key Functions (Python)

### `get_employee_details(name, dataframe)`
```python
details = get_employee_details("NATHANIEL FORD", df)
```
- Case-insensitive, partial-match search on `EmployeeName`  
- Raises `ValueError` for invalid input, `KeyError` if no match found  

### `safe_get_employee(name, dataframe)`
Wraps the above with full `try/except` logging — never crashes the program.

### `build_employee_dict(dataframe)`
Returns `{EMPLOYEE_NAME: [list_of_record_dicts]}` for O(1) lookups after building.

### `export_employee_to_zip(name, dataframe)`
Exports all records for `name` to:
```
Employee Profile/<NAME>_details.csv
Employee_Profile.zip
```

---

## Submission

1. Zip the entire `sf_salary_project/` folder:
   ```bash
   zip -r sf_salary_submission.zip sf_salary_project/
   ```
2. Push to GitHub and share the repository URL **or** submit the ZIP directly.
