# GeoTag Studio

A single-file, offline-capable image geotagging tool. Drop in a photo, see any GPS data it already has plotted on a map, or pick a location and write GPS coordinates straight into the image's EXIF data — all in the browser, no server or install required.

## Features

- **Drag-and-drop or click-to-browse** image upload (JPEG, PNG, WebP, TIFF)
- **Automatic GPS detection** — if a photo already has geotag data, it's parsed the moment you load it and the map flies straight to that location
- **Manual geotagging** — click anywhere on the map, search for a place name, or use your device's current location to drop a pin
- **Write GPS EXIF into JPEGs** — assign coordinates and download a geotagged copy of the original file, metadata intact
- **Metadata panel** — camera make/model, date taken, dimensions, file size, altitude, and raw EXIF (debug view)
- **Reverse geocoding** — resolves a human-readable address for the selected coordinates via OpenStreetMap Nominatim
- **Export options** — download the geotagged JPEG, a location JSON sidecar, or a GPX waypoint
- **Quick links** — open the selected point directly in Google Maps or OpenStreetMap

## Works offline

Everything except the live map tiles and the place-name search runs entirely offline. The libraries the app depends on (Leaflet, piexifjs, ExifReader) are bundled directly into the HTML file rather than loaded from a CDN, so:

- Opening a photo that already has GPS data and seeing it plotted → works offline
- Clicking the map / entering coordinates to geotag a photo → works offline
- Writing GPS EXIF into the image and downloading the result → works offline

The only things that need an internet connection are the map's background tiles (from OpenStreetMap) and place-name search / reverse geocoding (from Nominatim). Without a connection, the map area will be blank but the pin position and all coordinate/EXIF functionality still work correctly.

## Usage

1. Open `Geotag-Studio-Image-Geotagger.html` in any modern browser — no build step, no dependencies to install.
2. Drop in an image or click to browse for one.
3. If the image already has GPS data, it appears on the map automatically.
4. To add or change a location: click the map, search for a place, use "Use my location," or type coordinates in manually.
5. Download the geotagged JPEG (or JSON/GPX) from the export options.

## Tech stack

- React 18 (bundled)
- [Leaflet](https://leafletjs.com/) 1.9.4 for the map
- [piexifjs](https://github.com/hMatoba/piexifjs) for reading/writing JPEG EXIF (including GPS)
- [ExifReader](https://github.com/mattiasw/ExifReader) for broader EXIF metadata parsing
- Map tiles © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors
- Geocoding via [Nominatim](https://nominatim.openstreetmap.org/)

## Notes

- Non-JPEG images (PNG, WebP, TIFF) can't have EXIF written back into them in-browser the same way JPEGs can — for these, the tool downloads a JSON sidecar with the location data instead.
- All processing happens client-side; no image or location data is sent to any server other than the map tile provider and, if used, the search/geocoding requests.

## License

Map data © OpenStreetMap contributors, available under the [Open Database License](https://www.openstreetmap.org/copyright). Add your own project license here.
