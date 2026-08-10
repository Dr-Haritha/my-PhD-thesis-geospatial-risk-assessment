# Methodology

## Overview

This study applies Geographic Information Systems (GIS), Remote Sensing, and the Revised Universal Soil Loss Equation (RUSLE) to assess soil erosion risk across Gujarat, India. Soil erosion is one of the most significant forms of land degradation and can adversely affect environmental resources, agricultural productivity, infrastructure, and cultural heritage landscapes.

The methodology integrates climatic, soil, topographic, vegetation, and conservation management factors within a GIS environment to estimate average annual soil loss and identify areas susceptible to erosion.

---

## Methodological Workflow

```text
Data Collection
       ↓
Generation of RUSLE Factors
       ↓
Rainfall Erosivity Factor (R)
Soil Erodibility Factor (K)
Slope Length & Steepness Factor (LS)
Crop Management Factor (C)
Conservation Practice Factor (P)
       ↓
RUSLE Modelling
       ↓
Average Annual Soil Loss Estimation
       ↓
Classification of Erosion Risk
       ↓
Accuracy Assessment
       ↓
Archaeological Site Risk Assessment
```

---

## Soil Erosion and Cultural Heritage

Soil erosion is a natural geological process that contributes to landscape evolution and site formation. However, human interventions such as agriculture, construction activities, and vegetation removal accelerate erosion and increase soil loss.

Erosion caused by water and wind has been identified as a significant threat to archaeological stratigraphy and cultural heritage resources. Since many archaeological sites are located within agricultural landscapes, erosion may expose, damage, or completely remove archaeological deposits.

According to MacDonald (1990), a soil loss rate of one ton per hectare per year can lower the ground surface by approximately 0.4 mm annually. Over time, such losses can significantly impact fragile archaeological remains.

---

## Revised Universal Soil Loss Equation (RUSLE)

Soil erosion was calculated using the Revised Universal Soil Loss Equation (RUSLE) developed by Wischmeier and Smith (1978).

```text
A = R × K × LS × C × P
```

Where:

| Factor | Description |
|----------|-------------|
| A | Average Annual Soil Loss (t ha⁻¹ yr⁻¹) |
| R | Rainfall Erosivity Factor |
| K | Soil Erodibility Factor |
| LS | Slope Length and Steepness Factor |
| C | Crop Management Factor |
| P | Conservation Practice Factor |

Each factor was generated individually in ArcGIS Pro and subsequently multiplied to estimate annual soil loss.

---

# Generation of Thematic Layers

## 1. Rainfall Erosivity Factor (R)

Rainfall erosivity represents the effect of rainfall intensity, duration, frequency, and kinetic energy on soil detachment and transportation.

For this study, the Global Rainfall Erosivity (GlobalR) dataset was used.

The rainfall erosivity factor is calculated as:

```text
R = Σ Σ (EI30)k
```

Where:

```text
EI30 = ( Σ er vr ) I30
```

Where:

- EI30 = Rainfall erosivity
- er = Unit rainfall energy (MJ ha⁻¹ mm⁻¹)
- vr = Rainfall volume during a rainfall event (mm)
- I30 = Maximum 30-minute rainfall intensity (mm h⁻¹)

The unit rainfall energy is calculated as:

```text
er = 0.29 [1 − 0.72 e(-0.05ir)]
```

Where:

- ir = Rainfall intensity during the time interval (mm h⁻¹)

### Output

![Rainfall Erosivity Factor](Images/01-r-factor.png)

---

## 2. Soil Erodibility Factor (K)

Soil erodibility represents the susceptibility of soil to erosion.

Higher percentages of silt and sand generally increase erosion potential, while organic carbon improves soil stability and reduces erosion.

The K-factor is calculated using the Sharpley (1990) equation:

```text
KUSLE = KW = Fcsand × Fcl-si × ForgC × Fhisand
```

```text
K = {0.2 + 0.3 exp[-0.0256 SAN (1 − SIL/100)]}
```

```text
× ( SIL / (CLA + SIL) )^0.3
```

```text
× [1.0 − 0.25 C / (C + exp(3.72 − 2.95 C))]
```

```text
× [1.0 − 0.7 SN1 / (SN1 + exp(-5.51 + 22.9 SN1))]
```

Where:

- SAN = Sand (%)
- SIL = Silt (%)
- CLA = Clay (%)
- C = Organic Carbon Content
- SN1 = (1 − SAN/100)

Soil texture and organic carbon information were obtained from the Digital Soil Map of the World (DSMW).

### Output

![Soil Erodibility Factor](Images/02-k-factor.png)

---

## 3. Slope Length and Steepness Factor (LS)

The LS factor combines slope length and slope steepness.

Longer and steeper slopes increase runoff velocity and therefore increase erosion potential.

The LS factor was calculated using the Moore and Burch (1986) equation:

```text
LS = ( λ / 22.13 )m ( sinβ / 0.0896 )n
```

Where:

- λ = Slope length
- β = Slope angle
- m = 0.4
- n = 1.3

Slope length was derived from flow accumulation and cell size.

Cartosat Version 3 Digital Elevation Model (DEM) data were used to generate this factor.

### Output

![Slope Length and Steepness Factor](Images/03-ls-factor.png)

---

## 4. Crop Management Factor (C)

The crop management factor represents the influence of vegetation cover and land management practices on erosion.

The factor ranges between:

```text
0 = Completely protected soil
1 = Bare soil
```

The Normalized Difference Vegetation Index (NDVI) was used to estimate vegetation cover.

NDVI was calculated using Landsat 8 OLI imagery.

```text
NDVI = (NIR − R) / (NIR + R)
```

Where:

- NIR = Near Infrared Band
- R = Red Band

The Crop Management Factor was calculated as:

```text
C = (-NDVI + 1) / 2
```

### Outputs

![NDVI](Images/04-ndvi.png)

![Crop Management Factor](Images/05-c-factor.png)

---

## 5. Conservation Practice Factor (P)

The P-factor represents conservation measures implemented to reduce erosion.

Values range from:

```text
0 = Maximum protection
1 = No conservation practices
```

The factor was generated using a combination of:

- Slope percentage
- Land Use Land Cover (LULC)

### Conservation Practice Values

| LULC Class | Slope (%) | P Value |
|------------|------------|----------|
| Agriculture | < 7 | 0.27 |
| Agriculture | 7–11.3 | 0.30 |
| Agriculture | 11.3–17.6 | 0.40 |
| Agriculture | 17.6–26.8 | 0.45 |
| Agriculture | > 26.8 | 0.50 |
| Built-up | - | 0 |
| Waterbodies | - | 0 |
| All Other Classes | - | 1 |

### Output

![Conservation Practice Factor](Images/06-p-factor.png)

---

# Average Annual Soil Loss

After generating all five RUSLE factors, annual soil loss was calculated by multiplying the R, K, LS, C, and P layers.

```text
A = R × K × LS × C × P
```

The resulting soil loss dataset was reclassified into six erosion categories following Singh et al. (1992).

| Average Annual Soil Loss (t ha⁻¹ yr⁻¹) | Erosion Class |
|------------------------------------------|--------------|
| 0–5 | Slight |
| 5.001–10 | Moderate |
| 10.001–20 | High |
| 20.001–40 | Very High |
| 40.001–80 | Severe |
| >80 | Very Severe |

### Area Distribution

| Average Annual Soil Loss (t ha⁻¹ yr⁻¹) | Area (sq km) |
|------------------------------------------|-------------|
| 0–5 | 160131.36 |
| 5.001–10 | 10117.83 |
| 10.001–20 | 7985.58 |
| 20.001–40 | 6091.60 |
| 40.001–80 | 4380.34 |
| >80 | 7317.19 |

### Output

![Average Annual Soil Loss](Images/07-soil-loss-map.png)

---

# Accuracy Assessment

The soil erosion dataset was evaluated using a post-classification accuracy assessment.

A total of 90 random validation points were generated and compared with ground observations.

The confusion matrix is shown below.

| Erosion | Absent | Present | Total | User Accuracy |
|----------|---------|---------|---------|---------|
| Absent | 51 | 3 | 54 | 0.944 |
| Present | 9 | 27 | 36 | 0.750 |
| Total | 60 | 30 | 90 | - |

### Producer Accuracy

| Class | Accuracy |
|---------|----------|
| Absent | 0.85 |
| Present | 0.90 |
| Overall Accuracy | 0.868 |

### Kappa Coefficient

```text
Kappa = 0.719
```

According to McHugh (2012), kappa values between:

- 0.61–0.80 indicate substantial agreement
- 0.81–1.00 indicate almost perfect agreement

The obtained kappa value of 0.719 indicates substantial agreement between the model and ground observations.

---

# Archaeological Site Risk Assessment

To assess impacts on archaeological sites, areas experiencing soil loss greater than:

```text
20 t ha⁻¹ yr⁻¹
```

were considered high-risk zones.

These correspond to:

- Very High
- Severe
- Very Severe

erosion classes.

Site polygons and a 300 m buffer were overlaid with the soil erosion dataset to calculate the percentage of each site exposed to high-risk erosion zones.

Risk levels were assigned based on the proportion of site area affected.

### Results

Out of 508 archaeological sites:

| Risk Category | Number of Sites |
|---------------|----------------|
| Low Risk | 215 |
| Moderate Risk | 278 |
| High Risk | 15 |

The analysis identified a limited number of sites experiencing significant erosion pressure, primarily associated with:

- Sandy clay loam soils
- Sparse vegetation cover
- Limited conservation practices
- Stream-bank erosion
- Agricultural land use

---

## References

- Durigon, V. L., et al. (2014)
- MacDonald (1990)
- McHugh (2012)
- Moore & Burch (1986)
- Panagos et al. (2017)
- Parveen & Kumar (2012)
- Sharpley (1990)
- Singh et al. (1992)
- Wischmeier & Smith (1978)

---
