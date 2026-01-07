# Personal Finance Analyzer

A Streamlit dashboard for analyzing personal finance transactions exported from the Bluecoins app (CSV). It cleans and loads data into PostgreSQL, then visualizes accounts, expenses, income, and payment/receiving methods.

**Features:**

- Interactive Streamlit dashboard with Home, Data, Dashboard and Documentation tabs.
- Upload CSV (Bluecoins `transactions_list.csv`) and generate visualizations.
- ETL functions to extract, transform, and load data into PostgreSQL.
- Time-series views (daily/weekly/monthly) and category breakdowns.

**Requirements:**

- Python 3.9+
- PostgreSQL (or use the included Docker Compose stack)
- See `requirements.txt` for Python dependencies.

Quick start (local, virtualenv):

```bash
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
streamlit run scripts/app.py
```

Docker (recommended):

```bash
docker-compose up --build
# open http://localhost:8501
```

Usage:

- Export transactions CSV from Bluecoins (expected columns: `Type, Date, Name, Amount, Currency, Category, Account, Status`).
- Open the app, go to the Data tab, upload the CSV and click "Generate Dashboard".
- Use the sidebar filters to choose accounts and time view.

Database

- The app writes two tables (`raw_transactions` and `transactions`) to PostgreSQL. The default Docker Compose Postgres settings are:

- DB: `personal_finance_dashboard`
- USER: `postgres`
- PASSWORD: `password`
- Connection URI example: `postgresql://postgres:password@postgres:5432/personal_finance_dashboard`

Project structure

- `scripts/` - application code and ETL helpers (`scripts/app.py`, `scripts/database.py`, `scripts/read_queries.py`).
- `images/` - images used by the Streamlit app.
- `requirements.txt` - Python dependencies.
- `Dockerfile`, `docker-compose.yaml` - containerized run configuration.

Notes

- The `transform` function filters for rows where `Status == 'Reconciled'` and requires the expected CSV columns. Ensure exported CSV matches the expected schema.
- If you run without Docker, create the Postgres DB and update the connection URI in `scripts/app.py` or pass via environment variable.





