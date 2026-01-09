# Automated Shoreline Erosion Monitoring

## Overview

### Problem

The dynamic coastline adjacent to Kouchibouguac National Park and neighboring communities like Baie-Sainte-Anne, New Brunswick, is facing significant pressure from coastal erosion and changing environmental conditions. These shifts threaten sensitive dune systems, salt marshes, coastal habitats, and local infrastructure. Effective, frequent monitoring is vital for conservation efforts and community planning.

### Solution

This project implements a rapid, automated workflow using open-source software to detect and quantify shoreline changes. By leveraging RADARSAT Constellation Mission (RCM) Synthetic Aperture Radar (SAR) data, processed via SNAP and analyzed in QGIS, this solution provides a reliable method for tracking coastal evolution without the need for expensive commercial imagery.

## Datasets Used

* **Primary Data:** RADARSAT Constellation Mission (RCM) C-band SAR (GRD product).
   * Source: NRCan EODMS Portal.
   * Timeline: Comparative analysis between 2019 and 2023.
* **Contextual Data:** Sentinel-2 Optical Imagery (Optional Base Map).
   * Source: Copernicus Data Space Ecosystem.

## Architecture & Workflow

The solution follows a standard Earth Observation processing chain. For detailed, step-by-step technical instructions, please refer to the [Data Processing Workflow](WORKFLOW.md).

1. **SAR Pre-processing (SNAP):** Raw RCM GRD data was calibrated to Sigma0 backscatter, speckle-filtered (Lee Sigma 5x5), and georeferenced using Range-Doppler Terrain Correction.
2. **Shoreline Extraction (QGIS):** Processed GeoTIFFs underwent thresholding to separate land from water. These rasters were vectorized into polygons and subsequently converted into line features representing the shoreline for each timestamp.
3. **Change Analysis (QGIS):** The 2019 and 2023 shorelines were overlaid to identify erosion and accretion zones.

## Results 📊

The workflow successfully visualized shoreline changes along the Kouchibouguac coast. The map below illustrates the baseline shoreline (Blue, 2019) versus the current shoreline (Red, 2023).

* **Key Finding:** Measurable shoreline movement was detected in high-energy zones.
* **Quantification:** In the most significantly affected areas, we measured approximately 130 meters of shoreline regression over the observed period.

## Future Work 🚀

This project serves as a feasibility prototype. Future enhancements include:

* **Scaling:** Expanding the workflow to cover the entire Gulf of St. Lawrence coast.
* **Automation:** Scripting the processing pipeline using Python (`snappy` and `pyqgis`) for fully automated, near real-time monitoring.
* **Web Dashboard:** Developing an interactive web map for stakeholders to view erosion hotspots.
* **Predictive Modeling:** Integrating Machine Learning to predict future erosion risks based on historical wave action and sea-level rise projections.
