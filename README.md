# NCC Analytics (real data only)

A GitHub page that shows only numbers pulled from the NCC demo tenant (4258998).

## Pages
Overview, Handle Time, Call Outcomes, AI Summary, Data Sources.
The Data Sources page lists how each number is calculated and what is left out on purpose.

## How it works
1. A GitHub Action runs every 30 minutes (or when you click Run workflow).
2. It runs the files in `sql/` against BigQuery.
3. It saves counts and averages in `docs/data.json`.
4. The page in `docs/index.html` reads `data.json`.

Until the job succeeds, the page shows the snapshot built into `index.html` and says so in the top bar.

## The one secret
Name: `GCP_SA_KEY`
Where: Settings > Secrets and variables > Actions > New repository secret
What goes in it: the whole contents of a Google service account JSON key file with BigQuery Data Viewer on dataset `4258998` and BigQuery Job User on project `thrio-prod-4258998`.

## Known limits
- BigQuery only has a call after it is dispositioned. There are no live views.
- Wrap-up time includes the wait for the AI summary.
- Handle time ignores calls left undispositioned for over an hour.
- What NCC counts as a transfer is not yet confirmed.
