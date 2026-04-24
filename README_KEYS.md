# Place Search & API Keys

This project uses **Nominatim (OpenStreetMap)** for place search by default — it requires **no API key** but has usage policies and rate limits. For production use you should prefer a commercial provider.

## Providers & how to get keys

### 1) Nominatim (OpenStreetMap)
- No API key required.
- Usage policy: don't bulk-download, respect rate limits, use a local instance for heavy use.
- Example usage (already in code):
  `https://nominatim.openstreetmap.org/search?format=json&q=SEARCH_QUERY&addressdetails=1&limit=6`

### 2) Google Places / Maps
- Signup: https://console.cloud.google.com/
- Enable **Places API** and **Maps JavaScript API**.
- Create an API key, restrict it to your domain, and enable billing (Google offers a free tier).
- Example Autocomplete REST (Place Autocomplete):
  `https://maps.googleapis.com/maps/api/place/autocomplete/json?input=SEARCH&key=YOUR_KEY`
- To get place details (lat/lng) use Place Details endpoint with `place_id`.

### 3) Mapbox
- Signup: https://www.mapbox.com/
- Get an access token.
- Use Mapbox Geocoding API:
  `https://api.mapbox.com/geocoding/v5/mapbox.places/SEARCH.json?access_token=YOUR_TOKEN&limit=6`

## Recommendations
- For light/demo usage use **Nominatim** (no key).
- For production/autocomplete UX use **Google Places** or **Mapbox** and cache suggestions on your backend.
- Do not expose sensitive server-only keys in frontend; restrict keys by domain and usage.

