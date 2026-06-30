# Global-Career-Relocation-Analyzer
Build an end-to-end pipeline that ingests job postings and cost-of-living data, computes cost-adjusted metrics (comfort_score, qualification_match), and outputs a master dataset ready for Power BI
(comfort_score, qualification_match), and outputs a master dataset ready for analysis or visualization.

This repo is targeted at data analysts / data engineers building an end-to-end demo pipeline (Python + SQLite) and producing reproducible analyses.

Repo structure
etl/
fetch_data.py # fetch raw data (APIs or starter CSVs)
clean_transform.py # basic cleaning and normalization
compute_metrics.py # currency conversion, comfort_score, qualification_match
data/
raw/ # raw snapshots (ignored by .gitignore)
staging/ # cleaned staging CSVs
final/ # final master_compare.csv
db/
schema.sql # database schema (SQLite/Postgres compatible)
docs/
data_dictionary.md
assumptions.md
requirements.txt
.gitignore
README.md
Quickstart (local)
Create & activate a virtual environment

mac / Linux:
python -m venv venv
source venv/bin/activate
Windows PowerShell:
python -m venv venv
.\venv\Scripts\Activate.ps1
Windows CMD:
python -m venv venv
venv\Scripts\activate
Install dependencies

pip install -r requirements.txt
Set environment variables (optional — required only if you want to pull from APIs)

mac / Linux:
export ADZUNA_APP_ID=&quot;your_id&quot;
export ADZUNA_APP_KEY=&quot;your_key&quot;
export CANDIDATE_SKILLS=&quot;python,sql,statistics&quot;
Windows (PowerShell):
$env:ADZUNA_APP_ID=&quot;your_id&quot;
$env:ADZUNA_APP_KEY=&quot;your_key&quot;
$env:CANDIDATE_SKILLS=&quot;python,sql,statistics&quot;
Run the ETL steps in order

python etl/fetch_data.py
python etl/clean_transform.py
python etl/compute_metrics.py
Result

The pipeline writes data/final/master_compare.csv. Open it in Power BI or load it into SQLite/Postgres for SQL analysis.
Notes & best practices
Do not commit API keys or secrets. Use environment variables or a local .env (and add .env to .gitignore).
Keep raw snapshots in data/raw/YYYYMMDD/ for reproducibility.
Document every assumption in docs/assumptions.md (currency conversion method, weights for comfort_score, qualification matching logic).
Database
Use db/schema.sql to create the demo schema in SQLite or Postgres.
Example using SQLite + pandas (in a Python shell):
import pandas as pd
from sqlalchemy import create_engine
engine = create_engine(&quot;sqlite:///db/relocation.db&quot;)
df = pd.read_csv(&quot;data/final/master_compare.csv&quot;)
df.to_sql(&quot;master_compare&quot;, engine, if_exists=&quot;replace&quot;, index=False)
Analysis & visualization
Open data/final/master_compare.csv in Power BI Desktop (Get Data → CSV) or in a Jupyter notebook for further analysis.
Suggested static analyses to include in your portfolio:
Top 10 countries by comfort_score for a selected job
Salary distribution by experience level for 2 chosen countries
What-if table: effect of ±10% salary on comfort_score
Data dictionary & assumptions
docs/data_dictionary.md lists fields in master_compare.csv.
docs/assumptions.md explains the comfort_score formula and any placeholders (e.g., FX table).
How to contribute / run locally
Fork the repo and clone locally:
git clone git@github.com:yourusername/global-career-relocation.git
cd global-career-relocation
Create a branch, commit changes, and open a PR:
git checkout -b feature/etl-improvements
git add .
git commit -m &quot;Improve currency conversion&quot;
git push origin feature/etl-improvements
License
Add a license of your choice (e.g., MIT). Include a LICENSE file in the repo.

