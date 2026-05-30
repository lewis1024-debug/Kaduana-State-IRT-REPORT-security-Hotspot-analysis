# Kaduana-State-IRT-REPORT-security-Hotspot-analysis

# Kaduna State IRT Security Hotspot Analysis

**Project:** Spatial analysis of kidnapping incidents and security response mapping for Kaduna State, Nigeria 
**Data Source:** IRT 2024 Incident Records 
**Objective:** Visualize threat concentration, assess IRT operational impact, and support data-driven deployment decisions.

## **1. Project Overview**

The Intelligence Response Team (IRT) is a specialized tactical unit of the Nigeria Police Force deployed to combat banditry, kidnapping-for-ransom, and terrorism in Kaduna State. This project translates IRT 2024 incident data into actionable spatial intelligence. 

**Key outputs:**
1. `Kaduna_Hotspots_2024` — Kernel density heatmap of kidnapping incidents by LGA
2. `Kaduna_Major_Roads` — Filtered highway network showing ambush corridors
3. Integrated threat map for identifying high-risk LGAs: Birnin Gwari, Igabi, Chikun, Kaduna North, Kaduna South

This analysis supports the findings in: *Report: Impact of the Intelligence Response Team (IRT) on Security Issues in Kaduna State*

## **2. Tools & Dependencies**

| **Tool** | **Version** | **Purpose** |
| --- | --- | --- |
| QGIS | 3.34+ LTR | Core GIS, spatial analysis, map layout |
| QuickOSM Plugin | 2.2+ | Download OSM road/administrative data |
| LibreOffice Calc / Excel | Any | Data cleaning, CSV prep |
| OpenStreetMap | Live API | Highway network data |
| Natural Earth / GADM | v4.1 | LGA administrative boundaries |

## **3. Data Sources**

1. **IRT 2024 Incident Records** — CSV with fields: `incident_id`, `date`, `lga`, `latitude`, `longitude`, `incident_type`, `victims_rescued`
2. **Kaduna LGA Boundaries** — Shapefile from GADM Nigeria Level 2 Admin
3. **OSM Highway Data** — `highway=trunk, primary, secondary, tertiary` via Overpass API

> **Note:** Raw incident coordinates are anonymized to LGA centroids for operational security. Exact locations are not published.

## **4. Workflow: Reproducing the IRT Map**

### **Step 1: Data Preparation**
1. Clean IRT CSV: Remove duplicates, validate lat/long, standardize LGA names
2. Import to QGIS: `Layer > Add Layer > Add Delimited Text Layer` → Set Geometry CRS to `EPSG:4326`

### **Step 2: Generate Incident Heatmap**
1. `Processing Toolbox > Heatmap (Kernel Density Estimation)`
2. **Input**: IRT points layer
3. **Radius**: `15000` meters — reflects rural mobility patterns
4. **Pixel size**: `300` meters
5. **Output**: `Kaduna_Hotspots_2024.tif`
6. **Symbology**: Singleband pseudocolor, `Inferno` ramp, 70% opacity

### **Step 3: Download Major Roads**
1. Install QuickOSM Plugin: `Plugins > Manage and Install Plugins`
2. `Vector > QuickOSM > QuickOSM`
3. **Key**: `highway` | **Value**: Use `Show query` and paste:
