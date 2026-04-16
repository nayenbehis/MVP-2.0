# Biotech Catalyst Tracker

Track upcoming Phase 3 readouts, PDUFA dates, and AdComs for publicly traded biotech companies.

---

## Requirements

- Node.js 18+
- Python 3.11+
- A free [Supabase](https://supabase.com) account

---

## Setup

### 1. Supabase

1. Create a new project at supabase.com
2. Go to **SQL Editor** → paste the contents of `supabase/schema.sql` → click Run
3. Go to **Settings → API** and copy your **Project URL**, **anon key**, and **service_role key**

### 2. Environment variables

Edit `.env.local` in the project root:

```
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
```

Edit `python/.env`:

```
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-service-role-key
```

### 3. Python scrapers

```bash
cd python
pip3 install -r requirements.txt
python3 scrape_clinicaltrials.py   # seed catalyst data
python3 update_prices.py           # seed price data
```

### 4. Web app

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

---

## Running scrapers

| Script | What it does | Frequency |
|---|---|---|
| `scrape_clinicaltrials.py` | Phase 3 trials from ClinicalTrials.gov | Daily |
| `scrape_sec_edgar.py` | PDUFA/readout dates from 8-K filings | Weekly |
| `scrape_fda.py` | FDA AdCom calendar | Weekly |
| `update_prices.py` | Price, 52w high/low, setup scores | Daily |
| `run_all.py` | Runs all four in order | As needed |

You can also trigger any scraper from the **Admin** page in the UI.
