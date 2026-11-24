# URJA EV – Go-to-Market Analysis for an Electric Two-Wheeler in Mumbai

Capstone Project 1 (Dashboarding) · Python, pandas, scikit-learn, Tableau

URJA EV is a **hypothetical** new electric two-wheeler (E2W) brand. This project analyses the Mumbai E2W market (2020 – Oct 2026) to advise on where, to whom and how it should launch.

## Business questions
1. How big is the Mumbai E2W market and how fast is it growing?
2. Who are the competitors, and is the market open to a new brand?
3. Is public charging good enough for E2W owners?
4. Which customer segment should URJA EV target, at what price and positioning?
5. Is a launch a GO, and in which RTO area should it start?

## Data
| Dataset | Source | Type | Raw → Clean rows |
|---|---|---|---|
| Vehicle registrations (2020 – Oct 2026) | Vahan Dashboard, MoRTH | Real | 356 → 316 |
| Public charging stations | Kaggle (saketpradhan) | Real | 214 → 60 (Mumbai only) |
| Customer survey | Made up for this assignment | **Synthetic** | 435 → 397 |

> The survey is synthetic, so survey and segment insights demonstrate the method and do not describe real Mumbai residents.
> Raw CSVs are not included in this repo. Download them from the sources above, or place your own copies and update the paths in the notebook.

## Approach
1. **Load and inspect** the three raw datasets.
2. **Clean**: standardise RTO area and brand names, fix data types, remove non-two-wheeler rows (cars, buses, 3-wheelers), impute missing values, drop duplicates, fix swapped or out-of-Mumbai coordinates, parse text values like `55k` or `1.2L`, and remove non-Mumbai respondents.
3. **EDA**: yearly registrations and growth, brand and area share, start-ups vs legacy OEMs, charging stations per 100 E2Ws, survey demographics, interest drivers and correlations.
4. **Segmentation**: K-Means (k = 4, chosen using elbow and silhouette) on age, income, budget and profession, followed by a segment scoring model.
5. **Launch scorecard**: six pass/fail tests and a ranking of the three RTO areas.
6. **Export** tidy CSVs for the Tableau dashboard.

## Key findings
- **29,280** E2Ws registered in Mumbai (2020 – Oct 2026). Registrations peaked in 2024 (6,212) and have been broadly flat since.
- **Open market**: the top 3 brands hold only 44.4%. Ola fell from about 30% to about 6%, while Hero Vida rose to 22.9%. Legacy OEMs now hold 38.4% of yearly registrations.
- **Charging gap**: about **0.20 stations per 100 E2Ws** (Mumbai Central is the weakest at 0.16). Roughly half of survey respondents cannot charge at home.
- **Best segments**: *Affluent Tech Professionals* (score 0.73, budget about Rs 2.1 lakh) and *Core Salaried Scooter Switchers* (score 0.72, the largest group at 39.5%, budget about Rs 1.1 lakh).
- **Area ranking**: Mumbai West ranks first overall, East has the biggest demand but depends heavily on one brand (Odysse), and Central ranks last.

## Recommendation: conditional GO
- **Primary target**: Affluent Tech Professionals, premium model at about Rs 2 lakh with a free home charger.
- **Secondary target**: Core Salaried Scooter Switchers, Rs 1.0 – 1.3 lakh model with easy EMI.
- **Where**: start in Mumbai East, then West.
- **Charging** is the only failed test, so include a free home charger and a battery-swap partner in the offer.

## Limitations
- The survey is synthetic.
- EV share of all two-wheelers uses **assumed** values because petrol two-wheeler registrations were not available. Scorecard pass levels are also assumptions.
- Registrations are counted by RTO area, not owner residence, and 2026 has only 10 months.
- The charging dataset may be incomplete, and zones are inferred from coordinates.

## Tableau dashboard
A four-page interactive dashboard (market growth, competitor share, charging readiness, customer segments) is **in progress**. The notebook's last section exports the files it uses (`registrations_clean.csv`, `charging_stations_clean.csv`, `survey_clean.csv`, `yearly_summary.csv`, `brand_share_by_year.csv`, `segment_profiles.csv`, `area_infrastructure_summary.csv`, `area_ranking.csv`, `launch_scorecard.csv`, `ev_share.csv`).

## Tech stack
Python (pandas, NumPy, matplotlib, seaborn, scikit-learn), Jupyter Notebook, Tableau.

## How to run
```bash
git clone https://github.com/<your-username>/urja-ev-go-to-market-analysis.git
cd urja-ev-go-to-market-analysis
pip install -r requirements.txt
jupyter notebook Urja_EV_Final.ipynb
```
The notebook currently reads and writes files using Windows paths (`C:\Users\Shraddha\...`). Edit those paths to your own folders before running.

## Author
**Shraddha Mane** · [LinkedIn](https://www.linkedin.com/) · shraddhasanjaymane11@gmail.com
