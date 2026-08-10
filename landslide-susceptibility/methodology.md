# Methodology

## Overview

The landslide susceptibility assessment was carried out using Geographic Information Systems (GIS), Remote Sensing, Multi-Criteria Decision Making (MCDM), and the Analytical Hierarchy Process (AHP). The objective was to identify areas susceptible to landslides across Gujarat, India, by integrating topographic, geological, hydrological, climatic, environmental, and anthropogenic factors within a spatial modelling framework.

The methodology consisted of:

1. Generation of thematic layers
2. Reclassification of thematic layers
3. Analytical Hierarchy Process (AHP)
4. Weighted Overlay Analysis
5. Multicollinearity Analysis
6. Model Validation using ROC–AUC

---

# Landslide Conditioning Factors

Fifteen landslide conditioning factors were selected based on their influence on slope instability and landslide occurrence.

| No. | Parameter |
|------|------------|
| 1 | Elevation |
| 2 | Slope |
| 3 | Aspect |
| 4 | Curvature |
| 5 | Average Rainfall |
| 6 | Drainage Density |
| 7 | Topographic Wetness Index (TWI) |
| 8 | Stream Power Index (SPI) |
| 9 | Lithology |
| 10 | Soil Type |
| 11 | Geomorphology |
| 12 | Distance from Lineaments |
| 13 | Normalized Difference Vegetation Index (NDVI) |
| 14 | Land Use Land Cover (LULC) |
| 15 | Distance from Roads |

---

# Generation of Thematic Layers

## Elevation, Slope, and Aspect

Elevation, slope, and aspect were derived from the Cartosat Digital Elevation Model (DEM). These parameters influence terrain stability, runoff patterns, and gravitational forces acting on slopes.

## Curvature

Curvature was generated from the DEM and classified into concave, flat, and convex landforms. Curvature influences water accumulation, erosion, and soil movement processes.

## Average Rainfall

Average rainfall data for the period 2012–2022 were obtained from the Indian Meteorological Department (IMD) and used to represent rainfall-induced landslide triggering conditions.

## Drainage Density

Drainage density was derived from stream networks generated through flow accumulation analysis and calculated using the Euclidean Distance tool.

## Topographic Wetness Index (TWI)

TWI was used to estimate soil moisture accumulation and saturation potential.

**Formula**

```text
TWI = ln(α / tanβ)
```

Where:

- α = local upslope contributing area
- β = slope angle in radians

The upslope contributing area was calculated as:

```text
α = (Flow Accumulation + 1) × Cell Size
```

## Stream Power Index (SPI)

SPI represents the erosive power of flowing water.

**Formula**

```text
SPI = ln[(As + 0.001) × ((tanβ / 100) + 0.001)]
```

Where:

- As = flow accumulation
- β = slope

## Lithology

Lithology represents the geological composition of the terrain. Geological units were derived from geological datasets of Gujarat and classified according to their susceptibility to landslides.

## Soil Type

Soil types were obtained from the Digital Soil Map of the World (DSMW) and classified based on their physical characteristics and susceptibility to slope failure.

## Geomorphology

Geomorphological units were used to represent terrain characteristics and landform evolution processes influencing landslide occurrence.

## Distance from Lineaments

Lineament data were obtained from the Geological Survey of India (GSI). Euclidean distance analysis was used to calculate proximity to faults and fractures.

## Normalized Difference Vegetation Index (NDVI)

NDVI was used to represent vegetation cover and was derived from satellite imagery.

**Formula**

```text
NDVI = (NIR - Red) / (NIR + Red)
```

Where:

- NIR = Near Infrared Band
- Red = Red Band

## Land Use Land Cover (LULC)

LULC data were derived from ESA WorldCover 2021 and classified into:

- Tree Cover
- Built-up
- Cropland
- Bare/Sparse Vegetation
- Water Bodies

## Distance from Roads

Road network data were obtained from GSI datasets. Euclidean distance analysis was used to calculate the distance from roads, which are known to influence slope instability through excavation and construction activities.

---

# Reclassification of Thematic Layers

To standardize the thematic layers for susceptibility modelling, each parameter was reclassified into susceptibility classes based on its influence on landslide occurrence.

Reclassification methods included:

- Manual Interval Classification
- Natural Breaks (Jenks)
- Equal Interval Classification
- Supervised Classification
- Geological and Geomorphological Classification

Each class was assigned a susceptibility score ranging from low to high according to its relative contribution to landslide occurrence.

---

# Analytical Hierarchy Process (AHP)

The Analytical Hierarchy Process (AHP) was used to determine the relative importance of the fifteen conditioning factors.

A pairwise comparison matrix was developed using Saaty's scale of relative importance. The matrix was normalized and criteria weights were calculated from the principal eigenvector.

### Criteria Weights

| Parameter | Weight |
|------------|---------|
| Elevation | 0.0910 |
| Slope | 0.0809 |
| Aspect | 0.0738 |
| Curvature | 0.0600 |
| Average Rainfall | 0.0923 |
| Drainage Density | 0.1141 |
| TWI | 0.0734 |
| SPI | 0.0636 |
| Lithology | 0.0875 |
| Soil Type | 0.0917 |
| Geomorphology | 0.0586 |
| Distance from Lineaments | 0.0495 |
| NDVI | 0.0313 |
| Distance from Roads | 0.0279 |
| LULC | 0.0322 |

### Consistency Assessment

Consistency Index (CI):

```text
CI = (λmax - n) / (n - 1)
```

Consistency Ratio (CR):

```text
CR = CI / RI
```

Where:

- λmax = 17.18
- CI = 0.15
- CR = 0.09

Since CR < 0.10, the pairwise comparison matrix was considered acceptable and consistent.

---

# Weighted Overlay Analysis

The final landslide susceptibility map was generated through weighted overlay analysis by integrating all reclassified thematic layers using their AHP-derived weights.

**Formula**

```text
LS = Σ(Wi × Ri)
```

Where:

- LS = Landslide Susceptibility
- Wi = Criteria Weight
- Ri = Reclassified Score
- n = Number of Parameters

---

# Landslide Susceptibility Classification

The resulting susceptibility map was classified into five categories.

| Susceptibility Class | Area (sq. km) |
|----------------------|--------------:|
| Very Low | 12884.25 |
| Low | 54608.72 |
| Moderate | 119460.16 |
| High | 9070.00 |
| Very High | 0.87 |

---

# Multicollinearity Analysis

To evaluate the independence of the selected conditioning factors, a multicollinearity analysis was performed.

A total of 500 random points were generated across the landslide susceptibility map and used to calculate Variance Inflation Factor (VIF) and Tolerance (TOL).

Tolerance:

```text
TOL = 1 - R²
```

Variance Inflation Factor:

```text
VIF = 1 / TOL
```

Acceptance criteria:

| Indicator | Threshold |
|------------|-----------|
| VIF | < 10 |
| TOL | > 0.10 |

The calculated VIF and TOL values satisfied the recommended thresholds, indicating that the selected factors were independent and suitable for susceptibility modelling.

---

# Model Validation

The predictive performance of the landslide susceptibility model was evaluated using Receiver Operating Characteristic (ROC) analysis.

The Area Under the Curve (AUC) value obtained for the model was:

```text
AUC = 0.750
```

An AUC value of 0.750 indicates good predictive capability and demonstrates the reliability of the landslide susceptibility model.

---

# Software and Tools

- ArcGIS Pro
- ArcGIS Spatial Analyst
- Remote Sensing
- Cartosat DEM
- ESA WorldCover 2021
- Analytical Hierarchy Process (AHP)
- Multi-Criteria Decision Making (MCDM)
- Weighted Overlay Analysis
- ROC–AUC Validation
