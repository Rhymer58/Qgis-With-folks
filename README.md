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
## Day 8: Terrain


- Built a DEM/hillshade terrain map of Cherangani Hills around Kapcherop using the Copernicus GLO-30 30m DEM (ESA; free download, no login).
- Styled elevation with singleband pseudocolor using the cpt-city DEM_print ramp, with a separate hillshade layer set to Multiply blend mode for shadows.
- Added county boundaries from GADM 4.1 as no-fill white outlines, plus a custom compact folk-made SVG north arrow from the `north_arrows` folder.
- Layout items: title, elevation legend, scale bar, source note “Source: Copernicus DEM GLO-30 (ESA), 30m. County boundaries: GADM 4.1”, and RHYMER@2026 watermark.

## Day 8: NDVI

- Built an NDVI map of western Kenya from Landsat 8 Collection 2 Level 2 scene `LC08_L2SP_170059_20260930_02_T1`, acquired 30 Sep 2026 and downloaded via Microsoft Planetary Computer (no login needed).
- Applied scaled surface reflectance in the QGIS raster calculator to each band (digital number × 0.0000275 − 0.2), using B4 (red) and B5 (NIR), then calculated NDVI as (B5 − B4) / (B5 + B4).
- Clipped NDVI to county boundaries (GADM 4.1) using Clip by Mask. Added county labels and a Kenya inset overview.
- Used discrete 5-class symbology: bare, sparse, moderate, healthy, and dense.
- Source note: USGS Landsat 8 C2 L2.
- The map PDF, `NDVI Map for select region in kenya.pdf`, will be uploaded by the user.
