# Wayfarer — Trip Planner

A responsive, single-page trip itinerary planner prototype, ready for GitHub Pages.

## Publish

This repository uses the GitHub Actions workflow in `.github/workflows/pages.yml` to deploy the static site. In repository Settings → Pages, select **GitHub Actions** as the build and deployment source.

## Features

- Create trips and organize stop-by-stop itineraries by date
- Add, edit and remove places; reorder stops by drag and drop or controls
- Per-leg transport mode selector and approximate ETA/distance
- Open places and multi-stop routes in Google Maps
- OpenStreetMap map preview; optional Google Maps Embed API key in Map settings
- Browser-local persistence via localStorage

## Limitations

Place search uses demo data unless connected to Google Places API (New). Route geometry and journey estimates in the prototype are approximate; accurate live times require Google Routes API. Trips are saved in the current browser only; there is no account or cloud sync.

Do not commit passwords, private itinerary details, or unrestricted API keys.