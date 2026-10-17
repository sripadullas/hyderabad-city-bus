# Hyderabad Transit Intelligence

A GitHub Pages-ready city bus dashboard based on the supplied `HYD CITY BUSES(1).xlsx` workbook. It uses Leaflet + OpenStreetMap, Chart.js, and SheetJS.

## Features
- Preloaded route inventory from the workbook’s four route sheets\n- Fleet-type chart from the workbook’s Hyderabad BS-6 city fleet sheet (City Ordinary, Metro Express, Metro Deluxe)
- Workbook sheet/header/row inspection and common-column detection
- Searchable route explorer and route details
- Light/dark OpenStreetMap tile layers
- Direct-route and one-transfer journey search when stop sequences are available
- Stop mapping only for validated coordinates in the workbook
- Live GPS integration status and integration checklist
- Responsive desktop/mobile layout
- No fabricated route counts, route geometry, ETAs, or vehicle positions

## Data extracted from the supplied workbook
- Route explorer includes **414 route records** with origin and destination present across the `ROUTE 1-100`, `ROUTE 100-200`, `ROUTE 300-400`, and `ROUTE 500-600` sheets. Some route identifiers have multiple records/variants.
- The route stop lists are assembled from the `FROM`, `VIA`, and `TO` fields. Stop order follows the workbook text; it is not a separately verified stop timetable.
- Fleet chart counts from `HYD CITY BS-6 VEHICLE DATA`: **City Ordinary 93**, **Metro Express 183**, **Metro Deluxe 349**. These are counts parsed from the two city-fleet blocks in that sheet, not live operating-bus counts.
- The workbook does not supply valid stop latitude/longitude pairs or live GPS positions in the route sheets. Therefore route lines and bus markers are not fabricated; the map stays centered on Hyderabad until coordinate/GPS data is available.
- All 11 worksheet names are included in Data workspace. Use **Data workspace → Choose Excel workbook** to inspect an updated workbook. The bundled data loads automatically when the site opens.

The website uses the prepared `assets/hyd-data.js` file for its bundled route data. The original workbook itself is not uploaded into the site, so the extracted route and fleet data are the only source data shipped.

## Deploy to GitHub Pages
1. Unzip this project.
2. Create a new GitHub repository.
3. Upload `index.html`, `styles.css`, `app.js`, `README.md`, `.nojekyll`, and the entire `assets/` folder (including `hyd-data.js`) to the repository root.
4. In **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`, then Save.
5. Open the published Pages URL; the extracted route inventory loads automatically.

No build step or Python server is required. Third-party libraries load from CDNs, so internet access is required.

## Local testing
Open `index.html` in a modern browser, or use Python:
```bash
python -m http.server 8000
```
Then visit `http://localhost:8000`.

## Workbook fields recognized
Common variants are detected for:
- Route ID/number/name
- Stop name and stop sequence
- Category/service type
- Origin and destination
- Latitude and longitude
- Depot and first/last timing
- Distance and vehicle ID

For journey planning, the source must associate stops with routes and preferably include a stop sequence. For mapping, valid latitude/longitude values must be provided. Place names alone are not converted to coordinates. A real live-tracking feed requires an authorized operator API/GPS source and a secure backend proxy; do not place private credentials in this static site.
