# Labour Force Survey Analysis

This project analyzes Statistics Canada's Labour Force Survey (LFS) microdata for 2025. It looks at hourly wages by education, age group, industry, province and firm size. The main focus is how much more or less people at each education level earn compared with high school graduates. It uses a four-step workflow across Python (pandas) and PostgreSQL for loading and filtering, Excel for the analysis, Power BI for charts, and PowerPoint for the final presentation.

## Workflow

| Step | Tool | Purpose |
|------|------|---------|
| 1 | Python (pandas) & PostgreSQL | Load the 12 monthly files into one table, filter to employees with an hourly wage and export those 688,793 records to Excel |
| 2 | Excel | Turn the category codes into labels with the codebook, then calculate the weighted average wages, the education premium and the premium within each age group |
| 3 | Power BI | Two-page report with the average wages and the education premium |
| 4 | PowerPoint | Seven-slide presentation of the findings, limits and next steps |

## Data

- **Source:** Statistics Canada, *Labour Force Survey: Public Use Microdata File* (catalogue number 71M0001X)
- **DOI:** https://doi.org/10.25318/71M0001X-eng
- **Reference period:** January to December 2025 (12 monthly CSV files, `pub0125.csv` to `pub1225.csv`)
- **Size:** 1,364,679 records (roughly 114,000 per month) and 60 variables
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
│   ├── Data/                                # Monthly LFS PUMF files (Jan to Dec 2025)
│   └── Documents/                           # User guide, codebook and notes for users
├── reports/
│   ├── labour-force-wage-analysis.xlsx      # Excel summary tables (numbers only, no formulas)
│   ├── labour-force-wage-dashboard.pdf      # Power BI report (2 pages)
│   └── labour-force-wage-presentation.pdf   # PowerPoint presentation (7 slides)
├── notebook.ipynb                           # Loading, filtering and Excel export
├── requirements.txt
└── README.md
```

Running the notebook also creates a timestamped `wage_estimates_*.xlsx` file in the project root. It is listed in `.gitignore`, so it is not in the repository.

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
2. In the second cell of `notebook.ipynb`, change `db_url` to match your own PostgreSQL setup. Keep the `postgresql+psycopg2://` prefix so SQLAlchemy 2.1 and later use the installed driver.
3. The 12 monthly CSV files are already in `2025-CSV/Data/`. To refresh them, download the 2025 CSV files from Statistics Canada and replace them there.

### Run the notebook

Open `notebook.ipynb` in VS Code or Jupyter and run the cells in order. The last cell exports the respondent-level wage data to a timestamped `wage_estimates_*.xlsx` file in the project root.

## Results

The wages below are weighted averages for employees in the ten provinces.

### Method

- **Employees only:** Only employees with an hourly wage are included (`lfsstat` is 1 or 2 and `hrlyearn` has a value). That is 688,793 of the 794,297 employed people in the 12 files. The other 105,504 are self-employed or unpaid family workers, who have no hourly wage in the survey.
- **Hourly wage:** `hrlyearn` divided by 100, as the [user guide](2025-CSV/Documents/UserGuide_LFS_PUMF_2025_ENG.pdf) says. It is the usual hourly wage before taxes and includes tips, commissions and bonuses.
- **Weighted average:** I stacked the 12 monthly files together, as the user guide says to do for a yearly estimate. Each average is `sum(wage × FINALWT) / sum(FINALWT)`, where `FINALWT` is the survey weight, roughly the number of people each respondent represents.
- **Education premium:** How much more or less a group earns than high school graduates, as a percentage. In the age comparison, each age group is compared with high school graduates of the same age.

### Main Findings

The national average hourly wage for employees was $36.40. People with a bachelor's degree earn about 50% more than high school graduates, and people with a degree above a bachelor's earn about 74% more. People who did not finish high school earn about 13% to 16% less. The table has all seven education levels.

| Education Level | Average Hourly Wage | Premium vs High School Graduates |
|-----------------|--------------------:|---------------------------------:|
| 0 to 8 years | $24.79 | -12.79% |
| Some high school | $23.97 | -15.68% |
| High school graduate | $28.43 | 0.00% |
| Some postsecondary | $27.52 | -3.20% |
| Postsecondary certificate or diploma | $34.70 | +22.06% |
| Bachelor's degree | $42.59 | +49.82% |
| Above bachelor's degree | $49.52 | +74.21% |

People aged 25 to 64 were also compared with high school graduates of the same age group. The bachelor's premium goes from 28.6% at ages 25 to 29 to about 52% in the 50s and early 60s. The premium for a degree above a bachelor's goes from 35.4% at ages 25 to 29 to 83.2% at ages 60 to 64. Both dip at ages 40 to 44, to 35.9% and 51.2%. Every group in this comparison has at least 4,214 people in the sample.

The highest and lowest average hourly wages by age group, industry, firm size and province:

| Group | Highest | Lowest |
|-------|---------|--------|
| Age group | $42.72 at ages 45 to 49 | $18.29 at ages 15 to 19 |
| Industry | $55.89 in utilities | $20.98 in accommodation and food services |
| Firm size | $40.33 at firms with more than 500 employees | $29.00 at firms with fewer than 20 employees |
| Province | $37.95 in British Columbia | $30.16 in Prince Edward Island |

### Limitations

- The results show a link between education and pay, not that education causes it.
- Age is the only factor I held constant. Union status, job tenure, industry and gender also affect wages.
- Self-employed workers are left out because they have no hourly wage in the survey.
- The survey keeps the same homes in the sample for up to six months in a row, and the public file cannot match a person from one month to the next. Because of that, I did not calculate confidence intervals or significance tests, so I cannot say how precise the averages are.

### Reports

- [Power BI report](reports/labour-force-wage-dashboard.pdf) (PDF, 2 pages): the national average and the average wage by education level, firm size, province, age group and industry on page 1, and the education premium for all ages and by age group on page 2.
- [Presentation](reports/labour-force-wage-presentation.pdf) (PDF, 7 slides): the data, the findings, the limits and the next steps.
- [Excel workbook](reports/labour-force-wage-analysis.xlsx): the summary tables behind the charts, on three sheets (numbers only, no formulas).
