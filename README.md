# NDVI-VEGETATION-HEALTH-ANALYSIS-DENPASAR-BALI
# 🌿 Project 02 — NDVI Vegetation Health Analysis (Denpasar, Bali)

This project performs a complete **NDVI vegetation health analysis** using **Sentinel-2 Surface Reflectance (L2A)** for the Denpasar region.  
It is part of my Geospatial Analyst / Remote Sensing portfolio and demonstrates real-world EO data processing workflows.

---

## 📌 Overview

This project includes:

- 🛰 Loading multi-band Sentinel-2 GeoTIFF (B4, B8, SCL)  
- ☁ Cloud masking using SCL (codes 3,7,8,9,10,11)  
- 🌱 NDVI computation & normalization  
- 🧠 Adaptive classification using percentiles (Low → Very High)  
- 🗺 High-quality visualization with discrete colorbar + legend box  
- 🗂 Export:
  - NDVI GeoTIFF  
  - Classified NDVI GeoTIFF  
  - PNG map  
  - Vector polygons (GPKG)  
  - NDVI statistics (JSON)

All steps are executed using **Python + Rasterio + GeoPandas** in a reproducible conda environment.

---

## 📂 Project Structure

project02_ndvi_analysis/
│
├── notebooks/
│   └── project02_ndvi_full.ipynb          # Main NDVI analysis notebook
│
├── data/
│   ├── raw/                               # Input Sentinel-2 TIFF (B4,B8,SCL)
│   └── processed/                         # NDVI & classified TIFF outputs
│
├── outputs/
│   ├── maps/                              # PNG maps + NDVI statistics (JSON)
│   └── shapefiles/                        # Polygonized NDVI classes (GPKG)
│
└── README.md


---

## 🛰 Data Source — Sentinel-2 (L2A)

Exported via **Google Earth Engine**:

- **B4** (Red)
- **B8** (Near Infrared)
- **SCL** (Scene Classification Layer)

The notebook includes a full export script (GEE JavaScript).

---

## 🔬 Methodology

### **1. Preprocessing**
- Load B4, B8, SCL
- Handle reflectance scaling (×10000 → 0–1)
- Cloud masking using SCL codes:
clouds = [3, 7, 8, 9, 10, 11]


---

### **2. NDVI Calculation**

\[
NDVI = \frac{NIR - RED}{NIR + RED}
\]

Saved to:

data/processed/ndvi_denpasar.tif


Nodata = `-9999` for robust GDAL/QGIS handling.

---

### **3. NDVI Classification**

Adaptive thresholds from percentiles:

| Class | Description | Percentile |
|-------|-------------|------------|
| 1     | Low         | ≤ p10      |
| 2     | Moderate    | p10–p50    |
| 3     | High        | p50–p90    |
| 4     | Very High   | ≥ p90      |

Saved to:

data/processed/ndvi_classified.tif


---

### **4. Visualization**

Features:

- Discrete 4-color NDVI classification
- Vertical colorbar (Low → Very High)
- Legend box with category labels
- 300 DPI PNG export

Output:

outputs/maps/ndvi_classified_map.png


---

### **5. Polygonization**

Raster → vector (dissolve per class, optional simplify):

outputs/shapefiles/ndvi_denpasar_classes.gpkg


---

### **6. NDVI Statistics (JSON)**

Includes:

- NDVI min/max/mean
- Class pixel count

outputs/maps/ndvi_stats.json


---

## 🛠 Tools Used

- Python 3.10  
- Rasterio  
- GDAL  
- GeoPandas  
- NumPy  
- Matplotlib  
- SciPy  
- Google Earth Engine  

---

## ▶ How to Run

### **1. Activate environment**
```bash
conda activate geo
2. Start JupyterLab
bash
Salin kode
jupyter lab
3. Open notebook
bash
Salin kode
notebooks/project02_ndvi_full.ipynb
4. Place input TIFF
bash
Salin kode
data/raw/sentinel2_denpasar_*.tif
5. Run all cells
From top to bottom.

📸 Example Output (add your image)

outputs/maps/ndvi_classified_map.png
📊 Key Results (Example)
NDVI range: –0.34 → 0.69

NDVI mean: 0.15

Class distribution:

Low: 97k px

Moderate: 610k px

High: 2.44M px

Very High: 2.44M px

(Numbers vary depending on date and cloud coverage.)

📎 Repository
🔗 https://github.com/samuelifau/Flood-Risk-Analysis---Denpasar-Bali

💼 Skills Demonstrated
Earth Observation (EO) analysis

Raster processing with Rasterio

Cloud masking

NDVI vegetation index

Raster classification

Polygonization & vector processing

Map design & visualization

Geospatial Python automation

Portfolio-level documentation

🤝 Connect with Me
🔗 linkedin.com/in/samueli-fau

If you are working with EO, climate, ML for geospatial, or RLHF for mapping tasks — feel free to reach out!
