# Wayfarer — Trip Planner Project Brief

## Product goal

A clean, desktop-first responsive web app for people planning multi-day trips. Users should be able to organize a trip by date, add places, reorder them, and understand the trip between each consecutive stop.

## MVP user stories

1. As a traveller, I can create a trip with a name, destination, start date, and end date.
2. As a traveller, I can switch between dates and maintain a separate itinerary for each day.
3. As a traveller, I can search a list of places and add one to a day.
4. As a traveller, I can add a custom place name, add notes, and edit visit time/duration.
5. As a traveller, I can drag and drop stops or use up/down controls to reorder them.
6. As a traveller, I can select a transport mode for each leg (public transport, car, or walking).
7. As a traveller, I can see the stop pins and ordered route preview update when the itinerary changes.
8. As a traveller, I can open individual places or a multi-stop route in Google Maps.
9. As a traveller, I can keep multiple trips and have edits saved in the browser.

## Main screens and components

- **Trip sidebar:** trip list, create trip, current trip indicator.
- **Trip overview:** title, destination, dates, total places, share and trip actions.
- **Day switcher:** one tab per trip day, with a dot for days containing places.
- **Itinerary editor:** numbered stops, visit time, duration, notes, delete, drag/drop, and keyboard-accessible alternative reorder buttons.
- **Travel leg rows:** transport mode, estimated ETA/distance, and Google Maps directions link.
- **Route map panel:** pin markers, visual route, travel mode selector, Google Maps route link.
- **Map settings:** optional Google Maps Embed API key.

## Data model (first pass)

```text
Trip
- id
- title
- destination
- startDate
- endDate
- days[]

Day
- id
- date
- title
- stops[]

Stop
- id
- name
- category
- address
- latitude
- longitude
- visitTime
- durationMinutes
- notes
- transportModeToNextStop
- placeId (add when Places API is connected)
```

## Current prototype scope

The delivered `index.html` is a single-file app and needs no npm build step. It includes seeded Tokyo/Kyoto demo trips, trip creation/deletion/duplication, day tabs, place add/search against a local demo list, custom-place entry, editable stop time/duration/notes, drag/drop and up/down reordering, per-leg transport selectors, localStorage persistence, a Leaflet/OpenStreetMap route preview, and Google Maps search/directions links.

### Known prototype limitations

- The place search is a seeded demo dataset, not live Google Places search.
- Custom places use an approximate map pin. Real coordinates require Place Details/Geocoding.
- Without a Google Maps key, the map uses OpenStreetMap and draws straight lines between stops, not road-level directions.
- ETAs and distances without a connected Routes API are rough estimates. They must not be treated as navigation data.
- Google Maps Embed API can be enabled in Map Settings. Google Maps Platform APIs require an API key and appropriate Cloud project/billing setup.
- Data is stored in localStorage in the current browser only; there is no authentication or cloud sync.

## Recommended production architecture

- **Frontend:** React + TypeScript, responsive component system, accessible drag/drop controls.
- **Database/auth:** Supabase/PostgreSQL or Firebase for users, trips, days, and stops.
- **Place search:** Google Places API (New) Autocomplete / Place Details; store Google Place IDs and the coordinates required for a route.
- **Map:** Google Maps JavaScript API for the live map, interactive markers, bounds, and route geometry.
- **Travel time:** Google Routes API for each consecutive leg. Request driving, walking, and transit options where supported. Cache results carefully and provide a graceful fallback for unsupported transit coverage.
- **Security:** Restrict browser API keys by referrer and enabled APIs. Use a backend for server-side requests, rate limiting, caching, and any secret credentials.

## Suggested implementation phases

1. **Prototype (delivered):** local trips, editable itinerary, drag/drop, demo map and route links.
2. **Live place discovery:** Places API search/autocomplete, address and coordinate resolution, place details.
3. **Accurate travel legs:** Routes API calls for distance, travel duration, and route geometry by mode.
4. **Account & sync:** authentication, database persistence, sharing permissions, and conflict handling.
5. **Polish:** itinerary timing warnings, map/list synchronization, export to PDF/calendar, collaborative planning, and mobile-friendly day editing.

## API references

- Maps URLs: https://developers.google.com/maps/documentation/urls/get-started
- Maps Embed API: https://developers.google.com/maps/documentation/embed/embedding-map
- Google Maps Platform setup: https://developers.google.com/maps/get-started
- Places API: https://developers.google.com/maps/documentation/places/web-service/overview
- Routes API: https://developers.google.com/maps/documentation/routes