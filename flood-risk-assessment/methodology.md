# Methodology

## Overview

This project applies Geographic Information Systems (GIS), Remote Sensing, and Multi-Criteria Decision Analysis (MCDA) to assess flood susceptibility across Gujarat, India. The methodology integrates environmental, hydrological, and topographic factors using the Analytical Hierarchy Process (AHP) and Weighted Overlay Analysis to generate a flood susceptibility map.

---

## Methodological Workflow

The overall workflow consisted of the following stages:

```text
Data Collection
       ↓
Generation of Thematic Layers
       ↓
Reclassification
       ↓
Analytical Hierarchy Process (AHP)
       ↓
Weighted Overlay Analysis
       ↓
Flood Susceptibility Mapping
       ↓
Multicollinearity Analysis
       ↓
Flood Risk Assessment
       ↓
Model Validation
```

---

## Flood Susceptibility Parameters

Ten conditioning factors were selected based on their influence on flood occurrence and hydrological behaviour.

| Parameter                                     | Role in Flood Susceptibility                                                                           |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Clay Content                                  | Influences infiltration capacity, runoff generation, and soil water retention.                         |
| Distance from Rivers                          | Represents proximity to river channels and exposure to riverine flooding.                              |
| Distance from Roads                           | Indicates the influence of transportation infrastructure on drainage patterns and flood vulnerability. |
| Drainage Density                              | Reflects the concentration of stream networks and surface water flow characteristics.                  |
| Elevation                                     | Identifies low-lying areas that are more susceptible to water accumulation and flooding.               |
| Land Use Land Cover (LULC)                    | Represents surface characteristics affecting infiltration, runoff, and hydrological response.          |
| Normalized Difference Vegetation Index (NDVI) | Measures vegetation density and its influence on infiltration, evapotranspiration, and runoff.         |
| Rainfall Deviation                            | Represents spatial variability in rainfall distribution and flood-generating potential.                |
| Slope                                         | Influences runoff velocity, infiltration, and water accumulation patterns.                             |
| Topographic Wetness Index (TWI)               | Indicates the tendency of water accumulation and soil moisture distribution across the landscape.      |

---

## Data Preparation

Spatial datasets were collected from multiple sources and processed within ArcGIS Pro. All layers were projected to a common coordinate system, clipped to the Gujarat boundary, and converted to a consistent raster format for analysis.

The workflow involved:

* Data acquisition
* Data preprocessing
* Raster generation
* Reclassification
* Weighted overlay modelling
* Validation

---

## Generation of Thematic Layers

### Clay Content

Clay-rich soils generally exhibit lower infiltration rates and higher surface runoff, increasing flood susceptibility.

![Clay Content](Images/01-clay-content.png)

---

### Distance from Rivers

Areas located closer to river channels are more vulnerable to riverine flooding.

![Distance from Rivers](Images/02-distance-from-rivers.png)

---

### Distance from Roads

Road infrastructure can alter natural drainage pathways and influence flood behaviour.

![Distance from Roads](Images/03-distance-from-roads.png)

---

### Drainage Density

Drainage density represents the total stream length per unit area and influences water concentration patterns.

![Drainage Density](Images/04-drainage-density.png)

---

### Elevation

Lower elevations are generally more susceptible to flooding due to reduced drainage potential.

![Elevation](Images/05-elevation.png)

---

### Land Use Land Cover (LULC)

Different land-cover classes influence infiltration, evapotranspiration, and runoff generation.

![LULC](Images/06-lulc.png)

---

### Normalized Difference Vegetation Index (NDVI)

Normalized Difference Vegetation Index (NDVI) was used to quantify vegetation density.

NDVI was calculated as:

```text
NDVI = (NIR − Red) / (NIR + Red)
```

where:

* NIR = Near Infrared Band
* Red = Red Band

![NDVI](Images/07-ndvi.png)

---

### Rainfall Deviation

Rainfall deviation was used to represent spatial variability in rainfall distribution.

Formula:

```text
Rainfall Deviation (%) =
((Recorded Rainfall − Average Rainfall) × 100)
/ Average Rainfall
```

![Rainfall Deviation](Images/08-rainfall-deviation.png)

---

### Slope

Slope influences runoff velocity and water accumulation.

![Slope](Images/09-slope.png)

---

### Topographic Wetness Index (TWI)

TWI is widely used to estimate the tendency of water accumulation across a landscape.

Formula:

```text
TWI = ln ( α / tanβ )
```

where:

```text
α = (Flow Accumulation + 1) × Cell Size
β = Slope Angle
```

![Topographic Wetness Index](Images/10-twi.png)

---

## Reclassification

All thematic layers were reclassified into flood susceptibility classes before overlay analysis.

| Layer                                         | Reclassification Method |
| --------------------------------------------- | ----------------------- |
| Clay Content                                  | Natural Breaks (Jenks)  |
| Distance from Rivers                          | Natural Breaks (Jenks)  |
| Distance from Roads                           | Natural Breaks (Jenks)  |
| Drainage Density                              | Natural Breaks (Jenks)  |
| Elevation                                     | Manual Classification   |
| Land Use Land Cover (LULC)                    | Land Cover Categories   |
| Normalized Difference Vegetation Index (NDVI) | Natural Breaks (Jenks)  |
| Rainfall Deviation                            | Natural Breaks (Jenks)  |
| Slope                                         | Natural Breaks (Jenks)  |
| Topographic Wetness Index (TWI)               | Natural Breaks (Jenks)  |

---

## Analytical Hierarchy Process (AHP)

The Analytical Hierarchy Process (AHP) was used to determine the relative importance of each flood conditioning factor.

A pairwise comparison matrix was constructed following Saaty's methodology to evaluate the relative importance of each parameter influencing flood susceptibility. The matrix was normalized and criterion weights were derived to support weighted overlay analysis.

### Saaty's Pairwise Comparison Scale

| Value      | Interpretation         |
| ---------- | ---------------------- |
| 1          | Equal Importance       |
| 3          | Moderate Importance    |
| 5          | Strong Importance      |
| 7          | Very Strong Importance |
| 9          | Extreme Importance     |
| 2, 4, 6, 8 | Intermediate Values    |

The resulting pairwise comparison matrix was normalized to derive criterion weights for all flood conditioning factors.

---

## Consistency Assessment

The consistency of the AHP matrix was evaluated using the Consistency Index (CI) and Consistency Ratio (CR).

### Consistency Index (CI)

```text
CI = (λmax − n) / (n − 1)
```

where:

* λmax = Principal Eigenvalue
* n = Number of Criteria

### Consistency Ratio (CR)

```text
CR = CI / RI
```

where:

* CI = Consistency Index
* RI = Random Index

A Consistency Ratio (CR) less than 0.10 indicates acceptable consistency within the pairwise comparison matrix.

---

## Weighted Overlay Analysis

The final flood susceptibility map was generated using weighted overlay analysis.

General formulation:

```text
FS = Σ (wi × Ri)
```

where:

* FS = Flood Susceptibility
* wi = Weight of Criterion i
* Ri = Reclassified Rank of Criterion i

The weighted overlay integrated all thematic layers according to their relative importance derived from AHP, producing a continuous flood susceptibility surface across Gujarat.

---

## Flood Susceptibility Mapping

The resulting flood susceptibility surface was classified into five susceptibility classes:

* Very Low
* Low
* Moderate
* High
* Very High

These classes represent increasing levels of flood susceptibility and support spatial decision-making for risk management and planning.

![Flood Susceptibility Map](Images/11-flood-susceptibility-map.png)

---

## Multicollinearity Analysis

Multicollinearity analysis was performed to evaluate relationships among conditioning factors and assess redundancy within the model.

### Tolerance (TOL)

```text
TOL = 1 − R²
```

### Variance Inflation Factor (VIF)

```text
VIF = 1 / (1 − R²)
```

Interpretation:

* TOL > 0.10 indicates acceptable tolerance.
* VIF < 10 indicates the absence of significant multicollinearity.

The analysis was conducted to ensure the selected parameters contributed independently to the flood susceptibility model.

---

## Flood Risk Assessment

The validated flood susceptibility map was used to assess flood risk across archaeological sites in Gujarat. Archaeological site locations and associated buffer zones were overlaid on the flood susceptibility map to identify areas exposed to high and very high flood susceptibility.

This approach enabled the identification of sites requiring priority monitoring, conservation planning, and risk mitigation measures.

---

## Model Validation

Model performance was evaluated using Area Under the Curve (AUC) analysis.

AUC provides a quantitative measure of the predictive capability of the flood susceptibility model and is widely used for validating spatial prediction models. Higher AUC values indicate stronger predictive performance and greater reliability of the susceptibility assessment.

![AUC Validation](Images/12-auc-validation.png)

---

## Applications

The methodology can support:

* Flood Risk Assessment
* Disaster Risk Reduction
* Watershed Management
* Environmental Planning
* Infrastructure Planning
* Spatial Decision Support Systems
* Heritage Risk Assessment

---

## Software and Tools

* ArcGIS Pro
* ArcGIS Spatial Analyst
* Remote Sensing Data Processing
* Microsoft Excel
* Analytical Hierarchy Process (AHP)
* Multi-Criteria Decision Analysis (MCDA)
* Weighted Overlay Analysis

---

## Related Publication

Kadapa, H. (2025). *A Geospatial Assessment of Flood Risk to Archaeological Sites Using Multicriteria Decision Making and Analytical Hierarchy Process*. Geographia Technica, 20(1), 281–297.

Available at:
https://technicalgeography.org/index.php/on-line-first/533-19_kadapa
