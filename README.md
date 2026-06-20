AI & GIS-Based Flood Inundation and Risk Mapping

A geospatial workflow for identifying and mapping flood-prone zones in the Brahmaputra Valley, Assam, using AI-assisted rule-based classification combined with satellite-derived elevation, hydrological, and rainfall data — built entirely on Google Earth Engine and run via Google Colab.

OVERVIEW

This project models flood susceptibility by integrating three key parameters:

- Elevation — SRTM 30m Digital Elevation Model (low-lying areas are more flood-prone)
- Flow Accumulation — HydroSHEDS hydrological dataset (drainage convergence zones)
- Rainfall — CHIRPS daily gridded rainfall data (cumulative monsoon precipitation)

These layers are combined using an AI-inspired rule-based logic to generate a composite flood risk score, classifying the landscape into low, moderate, and high-risk zones. Results are validated against Sentinel-1 SAR imagery, since radar backscatter can detect standing water even through monsoon cloud cover.

DATASETS USED

- Elevation (DEM) — USGS SRTM — USGS/SRTMGL1_003
- Flow Accumulation — HydroSHEDS — WWF/HydroSHEDS/15ACC
- Rainfall — CHIRPS — UCSB-CHG/CHIRPS/DAILY
- SAR Validation — Sentinel-1 — COPERNICUS/S1_GRD
- Admin Boundary — FAO GAUL — FAO/GAUL/2015/level1

All datasets are streamed directly from the Earth Engine data catalog — no manual downloads required.

WORKFLOW

1. Define AOI — Brahmaputra Valley boundary (via FAO GAUL admin layer or custom geometry)
2. Load DEM and derive terrain layers (slope, hillshade)
3. Load flow accumulation layer for drainage analysis
4. Aggregate rainfall over a defined monsoon flood period
5. Apply rule-based AI classification combining elevation, flow accumulation, and rainfall thresholds into a composite risk score (0–3)
6. Reclassify into clean risk categories (Low / Moderate / High)
7. Convert raster to vector polygons for spatial analysis
8. Calculate area statistics (sq. km) per risk class
9. Validate against Sentinel-1 SAR imagery
10. Export results to Google Drive (raster + shapefile)

REQUIREMENTS

pip install geemap earthengine-api geopandas

You'll also need:
- A Google Cloud project registered with the Earth Engine API
- Earth Engine authentication (ee.Authenticate())

USAGE

1. Open the notebook in Google Colab
2. Run the setup cell and authenticate with your Earth Engine-linked Cloud project:
   ee.Initialize(project='your-project-id')
3. Run cells sequentially to generate the risk map, statistics, and exports
4. Exported files (GeoTIFF + Shapefile) will appear in your Google Drive under the specified folder

OUTPUTS

- Classified flood risk raster (GeoTIFF)
- Flood risk vector polygons (Shapefile)
- Area statistics per risk class (sq. km)
- Interactive HTML map
- SAR-based validation layer

TECH STACK

- Google Earth Engine (Python API)
- geemap
- geopandas
- Google Colab

APPLICATIONS

Disaster risk assessment, flood early-warning support, mitigation planning, and climate resilience studies for flood-vulnerable river basins.

NOTES

- Risk thresholds (elevation, rainfall, flow accumulation) are tuned for the Brahmaputra Valley's specific hydrology and may need adjustment for other basins.
- This is an educational/training project; thresholds are illustrative and should be refined with ground-truth validation before operational use.

LICENSE

Specify your license here (e.g., MIT).
