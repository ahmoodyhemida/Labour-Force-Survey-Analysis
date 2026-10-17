# Labour Force Survey Analysis

> **Status:** Work in progress. The 2025 data is loaded into PostgreSQL. Cleaning and analysis are next.

This project analyzes Statistics Canada's Labour Force Survey (LFS) microdata for 2025. It uses a five-stage workflow across Python (pandas) and PostgreSQL for loading, cleaning, and filtering, Excel for the analysis, Power BI for charts, and PowerPoint for the final presentation.

## Planned Analysis (Draft)

**How do hourly wages in Canada differ by education, age group, industry and province in 2025, and what wage premium does each education level earn?**

The question may be refined once the data has been cleaned and explored.

## Workflow

| Step | Tool | Purpose | Status |
|------|------|---------|--------|
| 1 | Python (pandas) & PostgreSQL | Load the 12 monthly files into one table, then clean, decode and filter the data | Raw load complete, cleaning not started |
| 2 | Excel | Weighted estimates, wage comparisons and scenario analysis | Not started |
| 3 | Power BI | Interactive charts and dashboard | Not started |
| 4 | PowerPoint | Findings, recommendations and limitations | Not started |

## Data

- **Source:** Statistics Canada, *Labour Force Survey: Public Use Microdata File* (catalogue number 71M0001X)
- **DOI:** https://doi.org/10.25318/71M0001X-eng
- **Reference period:** January to December 2025 (12 monthly CSV files, `pub0125.csv` to `pub1225.csv`)
- **Size:** 1,364,679 records (roughly 113,000 per month) and 60 variables
- **Licence:** [Statistics Canada Open Licence](https://www.statcan.gc.ca/en/reference/licence)

Adapted from Statistics Canada, Labour Force Survey: Public Use Microdata File, 2025, catalogue number 71M0001X. This does not constitute an endorsement by Statistics Canada of this product.

## Tools Used

- Python, pandas, SQLAlchemy and psycopg2
- PostgreSQL
- Excel
- Power BI
- PowerPoint

## Project Structure

```text
.
├── 2025-CSV/                 
│   └── Documents/            # User guide, codebook and record layout
|   └── Data/                 # Monthly LFS PUMF files (Jan to Dec 2025)
├── notebook.ipynb            # Loading and initial filtering
├── requirements.txt
└── README.md
```

## Setup

Run the commands below from the project root.

### Create a virtual environment

**macOS / Linux**

```bash
python3 -m venv venv
source venv/bin/activate
```

**Windows Command Prompt**

```bash
python -m venv venv
venv\Scripts\activate
```

**Windows PowerShell**

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

### Install dependencies

```bash
pip install -r requirements.txt
```

If you are not opening the notebook in VS Code, install Jupyter as well:

```bash
pip install jupyter
```

### Prepare the database and data

1. Start a local PostgreSQL server and update the connection string in the second cell of `notebook.ipynb`.
2. Download the 2025 CSV files from Statistics Canada and place them in `2025-CSV/Data/`.

### Run the notebook

Open `notebook.ipynb` in VS Code or Jupyter and run the cells in order.

## Results

Coming soon.
