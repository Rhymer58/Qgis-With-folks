# Week 1 GIS Project: Kenya in QGIS

My first week learning QGIS 3.34 LTR, documented layer by layer. Everything here was built from scratch as a self-taught beginner, with folk walking me through each step.

## What's in this project

### 1. Base map and data setup
- Added OpenStreetMap as a live basemap layer
- Loaded Kenya county boundaries (GADM 4.1, level 1, 47 counties, EPSG:4326)
- Loaded Kenya road network data, classified by route type (primary, secondary, unknown)
- Joined the KNBS 2019 census population figures to the counties with a CSV table join, including fixing two county name spelling mismatches so all 47 counties matched

### 2. Filtering and querying
- Filtered counties by name to isolate individual counties (Nairobi, Kisumu)
- Filtered by population to build the "Million Club" (counties with over 1 million people)
- Learned the difference between Categorized styling (one color per unique value) and Graduated styling (Jenks natural breaks for numbers)

### 3. Kenya counties population map
- Built a 6-class Jenks choropleth of the 2019 census population per county
- Learned why Jenks beats quantile breaks here: raw population outliers (Nairobi) cluster the classes honestly
- Exported the final print layout: title, legend, scale bar, north arrow, grid frame, source note

### 4. Nairobi county clip
- Selected Nairobi by name, exported it as its own layer
- Clipped the roads layer to Nairobi's boundary
- Styled the roads so major routes read clearly against minor ones

### 5. Kisumu buffer analysis (reprojection)
- Reprojected Kisumu county from geographic coordinates (EPSG:4326) to UTM (EPSG:32737) so distances are in meters
- Built 50km buffer zones around Kisumu, plus river statistics along Kisumu's rivers
- Discovered the classic beginner lesson: buffering in degrees gives wrong distances, reproject first
- Selected clinics inside the buffer using Select by Location (only 1 of 5 hospitals falls within 50km)

### 6. Geocoding clinics
- Geocoded a list of Kenyan clinics from a CSV into point coordinates
- Loaded them over the county map to see coverage against the buffer zones

## Files
- week1.qgz, the full QGIS project (relative paths, downloads and just works)
- shapefiles for counties, roads, rivers and buffers
- exported maps as PDF
- CSVs used for joins and geocoding

## Note on boundaries
County boundaries follow GADM / Kenya's admin claims. Disputed border areas (like the Ilemi Triangle) may be drawn differently in other data sources.

## Tools
QGIS 3.34 LTR, GADM 4.1 data, KNBS 2019 census, OpenStreetMap
