# negriluca.github.io

Personal portfolio — data & product engineering.

**Live:** https://negriluca.github.io/

## Projects

| Project | Case study | Code |
|---|---|---|
| Travel Insights — 2,051 travel packages scraped, normalised and visualised | [travel-insights.html](projects/travel-insights.html) | [travel-insights](https://github.com/NegriLuca/travel-insights) |
| Apt Website — production direct-booking platform for a Rome rental | [apt-website.html](projects/apt-website.html) | [apt-website](https://github.com/NegriLuca/apt-website) |
| Codice Immobiliare — Rome rental-yield scanner | [codice-immobiliare.html](projects/codice-immobiliare.html) | [codice-immobiliare](https://github.com/NegriLuca/codice-immobiliare) |

## Structure

```
.
├── index.html
├── 404.html
├── projects/
│   ├── travel-insights.html
│   ├── apt-website.html
│   └── codice-immobiliare.html
├── assets/
│   ├── css/style.css
│   ├── js/main.js
│   ├── data/                 # generated dashboard payloads (JSON)
│   └── img/                  # og card, favicon, apartment photos
├── sitemap.xml
└── robots.txt
```

The site is plain HTML/CSS/JS — no build step. Charts use Plotly (CDN) and the map uses
Leaflet + CARTO dark tiles (CDN).

## Preview locally

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

A plain `file://` open will not load the JSON dashboards because of fetch/CORS rules —
serve over HTTP.

## Regenerating the dashboard data

```bash
# Travel Insights
cd ../travel-insights
PORTFOLIO_DATA=../NegriLuca.github.io/assets/data python scripts/build_data.py

# Codice Immobiliare
cd ../codice-immobiliare
PYTHONPATH=src python -m immobiliare.market \
  --listings /path/to/Lista_Annunci_Immobiliare_2025 \
  --booking /path/to/properties_scraped_Roma.pkl \
  --out ../NegriLuca.github.io/assets/data/rome_rental_market.json
```

## Deploy

This repository is named `NegriLuca.github.io`, so GitHub Pages serves the `main` branch
from the repository root. Push, then check **Settings → Pages** (source: *Deploy from a branch*,
branch `main`, folder `/ (root)`).

The `.nojekyll` file is required so files/folders starting with `_` are served as-is.
