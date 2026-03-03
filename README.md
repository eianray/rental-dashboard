# Planetary Modeling — SW Portland Rental Market Intelligence

A professional rental market intelligence dashboard for property managers, tracking competitor pricing, vacancy rates, and unit availability across SW Portland.

## Live Demo
Deployed at: [planetarymodeling.com](https://planetarymodeling.com)

**Login credentials:**
- Username: `tyler`
- Password: `cascade2026`

---

## Features
- **Market Overview** — avg rent, vacancy rate, total units tracked, price trend
- **30-Day Trend Chart** — per-property rent trajectory (Chart.js)
- **Competitor Table** — sortable comparison across 6 properties
- **Unit Availability Grid** — filterable by type (Studio / 1BR / 2BR)
- **Vacancy Bar Charts** — visual vacancy comparison

## Stack
- Pure HTML/CSS/JS — no build step required
- Chart.js (CDN) for trend charts
- Google Fonts (Inter + Space Grotesk)
- Data stored as `data/market.json`

## Tracked Properties
1. Terwilliger Terrace — 7360 SW Barbur Blvd
2. River Heights — 5025 SW Corbett Ave
3. Shadow Hills — 2040 SW Vermont St
4. Town & Country Apartments — 4820 SW Barbur Blvd
5. Hilltop House Apartments — 3223 SW 11th Ave
6. The Frederick — 3050 SW 10th Ave

---

## Deploy to Cloudflare Pages

### First-time setup
1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com) → **Pages**
2. Click **Create a project** → **Connect to Git**
3. Select the `eianray/rental-dashboard` GitHub repository
4. Configure:
   - **Framework preset:** None
   - **Build command:** *(leave blank)*
   - **Build output directory:** `/` (root)
5. Click **Save and Deploy**
6. Set custom domain: `planetarymodeling.com` under **Custom Domains**

### Updating Data
Edit `data/market.json` and push to `main` — Cloudflare Pages will auto-deploy.

### Future: Automated Daily Updates
To wire up live scraping:
1. Set up an [Apify](https://apify.com) actor to scrape competitor listings
2. Use a GitHub Action (cron: `0 6 * * *`) to:
   - Fetch Apify results
   - Update `data/market.json`
   - Commit and push → triggers auto-deploy

---

## Data Format (market.json)
```json
{
  "lastUpdated": "ISO timestamp",
  "properties": [{
    "id": "slug",
    "name": "Property Name",
    "address": "...",
    "totalUnits": 84,
    "avgRent": 1685,
    "minRent": 1150,
    "maxRent": 2250,
    "vacancyRate": 4.8,
    "lastUpdated": "YYYY-MM-DD",
    "available": [{ "unit": "104", "type": "1BR", "bed": 1, "bath": 1, "rent": 1525, "sqft": 680, "available": "YYYY-MM-DD" }]
  }],
  "trendData": {
    "dates": ["YYYY-MM-DD", ...],
    "series": { "property-id": [rent, rent, ...] }
  }
}
```

---

*Built by Planetary Modeling. Sample/demo data — for production use, wire up Apify scraping.*
