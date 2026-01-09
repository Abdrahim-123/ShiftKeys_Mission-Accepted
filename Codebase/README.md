# Data Processing Workflow

This document details the methodology used to process RADARSAT Constellation Mission (RCM) satellite data. The workflow utilizes SNAP and QGIS to detect shoreline changes along the coast of northeastern New Brunswick, focusing on Kouchibouguac National Park and Baie-Sainte-Anne.

## 1. Data Acquisition

* **Source:** NRCan EODMS Portal
* **Satellite:** RADARSAT Constellation Mission (RCM)
* **Product Type:** Ground Range Detected (GRD)
* **Area of Interest:** Coastal region of northeastern New Brunswick (Kouchibouguac National Park / Baie-Sainte-Anne).

**Datasets Used:**

* **Baseline Image (Before):** RCM GRD image acquired in 2019.
* **Analysis Image (After):** RCM GRD image acquired in 2023.

## 2. SNAP Processing Workflow

The following preprocessing pipeline was executed using ESA SNAP Desktop (v12) for each RCM image to prepare the data for vector analysis.

1. **Import:** Loaded the `manifest.safe` file.
2. **Radiometric Calibration:**
   * Tool: Radar > Radiometric > Calibrate
   * Output: Sigma0 band
3. **Speckle Filtering:** Reduced inherent SAR noise.
   * Tool: Radar > Speckle Filtering > Single Product Speckle Filter
   * Filter: Lee Sigma
   * Window Size: 5x5
4. **Terrain Correction:** Corrected geometric distortions and projected the image.
   * Tool: Radar > Geometric > Terrain Correction > Range-Doppler Terrain Correction
   * DEM: SRTM 1Sec HGT (AutoDownload)
   * Projection: WGS84 / UTM (Auto)
   * Pixel Spacing: 20 meters
5. **Export:** Saved the final terrain-corrected raster as a GeoTIFF.

## 3. QGIS Analysis Workflow

Post-processing analysis was conducted in QGIS (v3.x) to extract shoreline vectors from the corrected rasters.

1. **Load Raster:** Imported the processed `_TC.tif` files.
2. **Vectorization (Polygonize):**
   * Tool: Raster > Conversion > Polygonize (Raster to Vector)
   * Function: Converted pixel values (land vs. water) into vector polygons.
3. **Geometry Extraction:**
   * Tool: Vector > Geometry Tools > Polygons to Lines
   * Function: Converted filtered land polygons into boundary lines representing the shoreline.
4. **Final Export:**
   * Saved the resulting layers as ESRI Shapefiles (`.shp`).
   * Outputs: `Shoreline_Before_LINE.shp` and `Shoreline_After_LINE.shp`.

These shapefiles serve as the primary inputs for the comparative change analysis and final map generation.
