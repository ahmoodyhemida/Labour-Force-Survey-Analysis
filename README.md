# Labour Force Survey Analysis

> **Status:** Work in progress. The 2025 data is loaded into PostgreSQL. Cleaning and analysis are next.

This project analyzes Statistics Canada's Labour Force Survey (LFS) microdata for 2025. It uses a five-stage workflow across Python (pandas) and PostgreSQL for loading, cleaning, and filtering, Excel for the analysis, Power BI for charts, and PowerPoint for the final presentation.

## Workflow

| Step | Tool | Purpose |
|------|------|---------|
| 1 | Python (pandas) & PostgreSQL | Load the 12 monthly files into one table, then clean, decode and filter the data |
| 2 | Excel | Weighted estimates, wage comparisons and scenario analysis |
| 3 | Power BI | Interactive charts and dashboard |
| 4 | PowerPoint | Findings, recommendations and limitations |

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
│   └── Documents/            # User guide, codebook and notes for users
|   └── Data/                 # Monthly LFS PUMF files (Jan to Dec 2025)
├── notebook.ipynb            # Loading, filtering and Excel export
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

`ipykernel` is included so the notebook runs in VS Code. To open it in a browser instead, install Jupyter as well:

```bash
pip install jupyter
```

### Prepare the database and data

1. Start a local PostgreSQL server. The notebook needs one running before it will connect.
2. In the second cell of `notebook.ipynb`, update the connection string. It appears twice, in the `%sql` line and in `create_engine`. Keep the `postgresql+psycopg2://` prefix so SQLAlchemy 2.1 and later use the installed driver.
3. The 12 monthly CSV files are already in `2025-CSV/Data/`. To refresh them, download the 2025 CSV files from Statistics Canada and replace them there.

### Run the notebook

Open `notebook.ipynb` in VS Code or Jupyter and run the cells in order. The last cell exports the respondent-level wage data to a timestamped `wage_estimates_*.xlsx` file in the project root. These files are about 20 MB each and are ignored by git.

## Results

Coming soon.
