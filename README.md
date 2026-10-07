# Content-Category-Performance-Dashboard
Build an interactive dashboard to evaluate the performance of different content categories.
# Content Category Performance Dashboard

Task 5 (Advanced): Evaluate how content categories perform and recommend where to invest.

Live dashboard: open `dashboard/index.html` locally, or enable GitHub Pages (Settings > Pages > deploy from `main`, root) and visit `/dashboard/`.

## Repository structure
| Path | Purpose |
|---|---|
| `data/raw/Dataset.csv` | Original data (8,790 titles) |
| `data/processed/` | Cleaned title-by-category table, category metrics, yearly trend |
| `src/analysis.py` | Cleaning, metric calculation, dashboard build |
| `dashboard/template.html` | Dashboard source (Chart.js) |
| `dashboard/index.html` | Generated, self-contained interactive dashboard |

Reproduce: `pip install -r requirements.txt && python src/analysis.py`

## Method (Task workflow)
1. Category metrics. `listed_in` holds several genres per title, so it is split into one row per title-category (42 categories; a title counts once per category). Metrics: titles, share of catalogue, movie share, distinct countries, recent share, rating mix.
2. KPI design. Titles in view, categories shown, top performer, highest momentum, average market reach.
3. Interactivity. Filters: content type, rating group, country, year-added range, minimum titles, ranking metric. Scorecard columns are sortable.
4. High performers. Performance Index = 50% volume + 25% market reach + 25% momentum, each min-max scaled across categories with at least 30 titles. Top quartile is flagged green.
5. Recommendations. Below.

## Assumptions and limits
- The dataset has no viewership, revenue or engagement fields. "Performance" is therefore a catalogue-based proxy (investment volume, geographic breadth, recent acquisition momentum), not audience demand. Validate with viewing data before committing budget.
- Primary country = first country listed. Titles with no country are labelled Unknown.
- Momentum = share of a category's titles added in the final 3 years of the selected window. 2021 is a partial year (data ends September 2021).
- Rating groups: Kids (TV-Y, TV-Y7, TV-Y7-FV, TV-G, G), Teen/Family (TV-PG, PG, PG-13, TV-14), Mature (TV-MA, R, NC-17), Unrated/Other (NR, UR).
- Index weights are a judgment call and are easy to change in `src/analysis.py` and the dashboard script.

## Key findings
- Top performers (index): International Movies (87.0), Dramas (81.5), Comedies (64.9), International TV Shows (56.6), Action & Adventure (46.7). International Movies and Dramas reach 75 and 70 countries, respectively.
- Highest momentum (categories with 30+ titles): Classic Movies (82% of titles added in the last 3 years), Teen TV Shows (80%), Reality TV (76%), Cult Movies (75%), Anime Series (74%).
- Weak spots: lowest Performance Index scores are the generic Movies tag (1.8), Stand-Up Comedy & Talk Shows (7.3), Science & Nature TV (10.8), Stand-Up Comedy (12.7) and British TV Shows (16.0). Documentaries (47% recent share) and Stand-Up Comedy (38%) show the slowest recent acquisition among large categories.
- Audience mix: Children & Family Movies is 52% Kids-rated and Kids' TV 91%, so they serve a distinct audience from the Mature-heavy drama and crime categories.
- Catalog additions peaked in 2019 (2,016 titles) and fell in 2020 (1,879) and 2021 (1,498, partial year).

## Recommendations
1. Protect the core. Keep International Movies and Dramas as anchor categories. Breadth across 70+ markets makes them the safest base for retention.
2. Scale momentum categories selectively. Reality TV and Anime Series are growing fast but Anime reaches only 7 countries. Test regional expansion for Anime before increasing volume.
3. Fix or prune low performers. Stand-Up Comedy and Documentaries have large catalogs but ageing acquisition. Refresh with newer titles or reduce spend, subject to viewing data.
4. Clean the taxonomy. The generic "Movies" tag and overlapping Stand-Up labels weaken reporting. Standardise category tags.
5. Cover the family segment deliberately. Kids' TV and Children & Family Movies are a separate audience. Track them with their own KPIs, not against Mature drama.
6. Add engagement data. Join viewing hours, completion rate and cost per title, then re-weight the index on actual demand.


