# Teaching DRRAA Weather Radar & GIS

[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Google Colab](https://img.shields.io/badge/Google-Colab-F9AB00.svg?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![Py-ART](https://img.shields.io/badge/Radar-Py--ART-4C8BF5.svg)](https://arm-doe.github.io/pyart/)
[![GeoPandas](https://img.shields.io/badge/GIS-GeoPandas-139C5A.svg)](https://geopandas.org/)
[![pyhail](https://img.shields.io/badge/Hail-pyhail-6A5ACD.svg)](https://github.com/joshua-wx/pyhail)

> **แบบเรียนเชิงปฏิบัติการด้านเรดาร์ตรวจอากาศ–ภูมิสารสนเทศ สำหรับการวิเคราะห์ฝน พายุรุนแรง และลูกเห็บในประเทศไทยด้วย Python และ Google Colab**

Repository นี้พัฒนาขึ้นเพื่อใช้เป็นแบบเรียนแบบ **step-by-step** สำหรับนิสิตระดับปริญญาตรีชั้นปีที่ 3–4 และระดับบัณฑิตศึกษาในสาขา **ภูมิศาสตร์ ภูมิสารสนเทศ วิทยาศาสตร์สิ่งแวดล้อม อุตุนิยมวิทยา และสาขาที่เกี่ยวข้อง** โดยใช้ข้อมูลเรดาร์ตรวจอากาศจริงร่วมกับข้อมูล GIS และข้อมูลอุตุนิยมวิทยาชั้นบน

หลักสูตรปัจจุบันสิ้นสุดที่ **Notebook 10A — GIS Exposure and Administrative Analysis** และครอบคลุมกระบวนการตั้งแต่การอ่านข้อมูลเรดาร์ดิบ ไปจนถึงการวิเคราะห์พายุแบบสามมิติ การประมาณฝน การวิเคราะห์ลูกเห็บ และการเชื่อมผลิตภัณฑ์เรดาร์กับหน่วยการปกครองด้วย GIS

---

## Course philosophy

แนวคิดหลักของแบบเรียนคือ

```text
Radar Measurement
      ↓
Radar Geometry
      ↓
Spatial Representation
      ↓
Meteorological Variable
      ↓
GIS Integration
      ↓
Environmental Quantity
      ↓
Spatial / Temporal Analysis
      ↓
Scientific Interpretation
```

นักศึกษาจะไม่ได้เรียนเพียง “วิธี plot เรดาร์” แต่จะเรียนรู้ว่า **ข้อมูลที่เรดาร์วัดจริงคืออะไร การประมวลผลแต่ละขั้นเพิ่มสมมติฐานอะไรเข้าไป และควรตีความผลลัพธ์ทางวิทยาศาสตร์อย่างไร**

หลักการสำคัญที่ใช้ตลอดหลักสูตร:

- **PPI ≠ CAPPI**
- **dBZ ≠ rainfall**
- **radial velocity ≠ total wind speed**
- **Cartesian grid ≠ original radar observation**
- **Radar QPE ≠ ground truth**
- **GIS overlay ≠ physical validation**
- **Echo top ≠ cloud top**
- **Radar echo base ≠ cloud base**
- **High reflectivity ≠ proof of hail**
- **MESH / SHI / POSH ≠ observed hail truth**
- **Fine grid spacing ≠ fine observational resolution**
- **Thresholds developed elsewhere are not automatically valid for Thailand**

---

## Learning objectives

เมื่อเรียนครบ Notebook 01–10A ผู้เรียนควรสามารถ:

1. อ่านและตรวจสอบข้อมูลเรดาร์ตรวจอากาศแบบ UF ด้วย Python
2. เข้าใจโครงสร้าง radar volume, sweep, ray และ gate
3. วิเคราะห์ reflectivity, Doppler velocity และ dual-polarization variables เบื้องต้น
4. อธิบาย radar beam geometry และข้อจำกัดจากระยะทางและ elevation angle
5. แปลงข้อมูล polar radar เป็น Cartesian 3-D grid และ CAPPI
6. ใช้ CRS, map projection และ GeoTIFF เชื่อมข้อมูลเรดาร์กับ GIS
7. แปลง reflectivity เป็น rainfall rate และ event accumulation ด้วย Z–R relations
8. คำนวณ point extraction และ zonal statistics
9. วิเคราะห์ vertical storm structure, pseudo-RHI และ cross-section
10. คำนวณ echo tops, VIL, VILD, severe-core area และ echo volume
11. ใช้ SHI, MESH และ POSH เพื่อศึกษาศักยภาพของลูกเห็บอย่างมีข้อจำกัด
12. วิเคราะห์ storm lifecycle แบบบูรณาการ
13. เชื่อมผลิตภัณฑ์ severe storm/hail กับ ADM1 และ ADM2
14. สร้าง storm-core track และ administrative exposure
15. แยก **observation, retrieval, interpolation, exposure และ interpretation** ออกจากกันอย่างถูกต้อง
16. สร้าง output ที่ reproducible และเหมาะสำหรับต่อยอดงานวิจัย

---

## Main scientific libraries

| Library | Role in this course | Link |
|---|---|---|
| **Py-ART** | อ่านข้อมูลเรดาร์, PPI, Doppler processing, Cartesian gridding | https://arm-doe.github.io/pyart/ |
| **pyhail** | SHI, MESH, POSH และ hail-related retrievals | https://github.com/joshua-wx/pyhail |
| **NumPy** | Numerical array processing | https://numpy.org/ |
| **Pandas** | Tables, metadata, lifecycle and statistics | https://pandas.pydata.org/ |
| **Matplotlib** | Scientific visualization | https://matplotlib.org/ |
| **SciPy** | Filtering, statistics and scientific utilities | https://scipy.org/ |
| **GeoPandas** | Vector GIS and administrative boundaries | https://geopandas.org/ |
| **Shapely** | Geometry operations | https://shapely.readthedocs.io/ |
| **Rasterio** | GeoTIFF and raster GIS operations | https://rasterio.readthedocs.io/ |
| **PyProj** | CRS and coordinate transformation | https://pyproj4.github.io/pyproj/ |
| **Cartopy** | Geographic plotting and map projections | https://scitools.org.uk/cartopy/ |

Notebook แต่ละไฟล์ติดตั้ง package ที่จำเป็นใน Google Colab โดยตรง ดังนั้นผู้เรียนไม่จำเป็นต้องติดตั้ง Python environment ในเครื่องก่อนเริ่มเรียน

---

## Data used in the course

### 1. Weather radar

กรณีศึกษาหลักใช้ข้อมูล **S-band weather radar, Omkoi, Thailand** ในเหตุการณ์ลูกเห็บวันที่ **18 March 2023**

Radar metadata ที่ใช้ในหลักสูตร:

```text
Radar site       : Omkoi
Latitude         : 17.798207°N
Longitude        : 98.432326°E
Altitude         : 1,173 m MSL
Radar band       : S-band
Scan type        : PPI
Sweeps           : 14
Gate spacing     : 500 m
Maximum range    : ~237 km
Event period     : approximately 11:06–12:00 UTC
Number of scans  : 10 volumes
```

ตัวอย่าง radar fields:

```text
corrected_reflectivity
corrected_differential_reflectivity
cross_correlation_ratio
differential_phase
specific_differential_phase
velocity
spectrum_width
```

Primary hail-event data directory:

[`2023031810UTCลูกเห็บ/`](https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/tree/main/2023031810UTC%E0%B8%A5%E0%B8%B9%E0%B8%81%E0%B9%80%E0%B8%AB%E0%B9%87%E0%B8%9A)

Repository ยังมี radar dataset อื่นสำหรับการทดลอง/เปรียบเทียบเพิ่มเติม แต่ workflow หลักของ Notebook 01–10A ใช้ observed-hail event ข้างต้นเป็นกรณีศึกษา

### 2. Upper-air sounding

Notebook 08 ใช้ radiosonde จาก **Dien Bien Phu, Vietnam — WMO 48811, 00 UTC 18 March 2023** เป็น **remote observed sounding proxy** เนื่องจากไม่มี upper-air sounding ที่อยู่ใกล้ Omkoi และตรงกับเวลาพายุ

[`2023031800-48811_sounding_Vietnam.csv`](https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/2023031800-48811_sounding_Vietnam.csv)

Sounding ใช้ derive:

```text
0°C level
−10°C level
−20°C level
−30°C level
```

โดย 0°C และ −20°C levels ถูกใช้ใน SHI/MESH workflow

> **Important:** sounding นี้เป็น observed profile จริง แต่เป็น **off-site environmental proxy** ไม่ใช่ local storm sounding จึงต้องรายงาน spatial and temporal representativeness uncertainty ทุกครั้งที่ใช้ MESH ในการตีความเชิงวิจัย

### 3. Administrative GIS

ขอบเขตประเทศไทยใช้ข้อมูล **geoBoundaries**:

- ADM0 — national boundary
- ADM1 — province
- ADM2 — district/amphoe, simplified version for teaching

Repository files:

- [`geoBoundaries-THA-ADM0.geojson`](https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/geoBoundaries-THA-ADM0.geojson)
- [`geoBoundaries-THA-ADM1.geojson`](https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/geoBoundaries-THA-ADM1.geojson)
- [`geoBoundaries-THA-ADM2_simplified.geojson`](https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/geoBoundaries-THA-ADM2_simplified.geojson)

Source: **geoBoundaries / gbOpen**  
License: **CC BY 4.0**

ADM2 ถูก simplify เพื่อใช้ในการเรียนและ visualization ดังนั้น zonal statistics อาจแตกต่างจากขอบเขตความละเอียดเต็ม

---

## Course workflow

```text
01  Data Audit
 │
02  PPI + Beam Geometry + Doppler
 │
03  3-D Grid + CAPPI + CRS
 │
 ├───────────────────────┐
 │                       │
04  Z–R QPE              06  Vertical Storm Structure
 │                       │
05  Rain Accumulation    07  ET / VIL / VILD / Core Metrics
 │                       │
 └───────────┬───────────┘
             │
            08
      SHI / MESH / pyhail
             │
            09A
   Integrated Event Analysis
             │
            10A
 GIS Exposure & Administrative Analysis
```

มีสองแกนการเรียนที่เชื่อมกัน:

```text
Hydrology / QPE
03 → 04 → 05

Severe Storm / Hail
03 → 06 → 07 → 08

Integrated research workflow
09A → 10A
```

---

## Notebooks

<table>
<thead>
<tr>
<th>No.</th>
<th>Notebook</th>
<th>Purpose</th>
<th>Core theory / concepts</th>
<th>Learning outcomes</th>
<th>Open</th>
</tr>
</thead>
<tbody>
<tr>
<td><b>01</b></td>
<td><b>Radar & GIS Data Audit</b><br><sub>01_get_and_understand_DRRAA_radar_GIS_data.ipynb</sub></td>
<td>ทำความเข้าใจโครงสร้างข้อมูลเรดาร์ UF, metadata, sweep geometry, fields, เวลา UTC และข้อมูลขอบเขตการปกครอง ก่อนเริ่มการวิเคราะห์</td>
<td>Radar volume, sweep, ray, gate, radar moments, metadata, event audit, GIS layer structure</td>
<td>อ่าน UF และ GIS ได้, ตรวจ metadata ได้, แยก sweep/ray/gate ได้, ตรวจความพร้อมของ event dataset ได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/01_get_and_understand_DRRAA_radar_GIS_data.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/01_get_and_understand_DRRAA_radar_GIS_data.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>02</b></td>
<td><b>PPI, Radar Moments, Beam Geometry & Doppler Evolution</b><br><sub>02_PPI_radar_moments_beam_geometry_and_Doppler_evolution.ipynb</sub></td>
<td>วิเคราะห์โครงสร้างพายุใน polar coordinates จากหลาย elevation angles พร้อม Doppler velocity QC และการติดตามการเปลี่ยนแปลงของเหตุการณ์ลูกเห็บ</td>
<td>PPI, reflectivity, radial velocity, beam height, 4/3 Earth model, velocity dealiasing, dual-pol quicklook</td>
<td>อ่าน PPI หลายมุมยกได้, คำนวณ beam height ได้, เข้าใจ radial velocity, ทำ velocity QC เบื้องต้น และอธิบาย storm evolution ได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/02_PPI_radar_moments_beam_geometry_and_Doppler_evolution.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/02_PPI_radar_moments_beam_geometry_and_Doppler_evolution.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>03</b></td>
<td><b>Cartesian Grid, CAPPI, CRS & GIS</b><br><sub>03_Cartesian_Grid_CAPPI_CRS_and_GIS.ipynb</sub></td>
<td>แปลงข้อมูลเรดาร์จาก polar coordinates ไปสู่ 3-D Cartesian grid เพื่อสร้าง CAPPI และเชื่อมโยงกับระบบพิกัด GIS</td>
<td>Polar-to-Cartesian gridding, CAPPI, interpolation, ROI, MSL/ARL, AEQD, UTM, CRS</td>
<td>สร้าง 3-D radar grid และ CAPPI ได้, อธิบาย interpolation/ROI ได้, แยก MSL กับ ARL ได้ และเชื่อมข้อมูลเรดาร์กับ CRS ทาง GIS ได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/03_Cartesian_Grid_CAPPI_CRS_and_GIS.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/03_Cartesian_Grid_CAPPI_CRS_and_GIS.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>04</b></td>
<td><b>Z–R QPE & Spatial Point Extraction</b><br><sub>04_ZR_QPE_and_Spatial_Point_Extraction.ipynb</sub></td>
<td>แปลง reflectivity เป็น rainfall rate ด้วยสมการ Z–R หลายแบบและฝึกการดึงค่าที่จุดระหว่าง native radar gate กับ Cartesian CAPPI</td>
<td>dBZ → Z → rainfall rate, Z–R relation, QPE sensitivity, NoData, point extraction, GeoTIFF</td>
<td>คำนวณ radar QPE ได้, เปรียบเทียบ Z–R relations ได้, แยก zero rainfall กับ NoData ได้ และดึงค่าจาก raster/เรดาร์ที่ตำแหน่งสนใจได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/04_ZR_QPE_and_Spatial_Point_Extraction.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/04_ZR_QPE_and_Spatial_Point_Extraction.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>05</b></td>
<td><b>Event-Centered Rainfall Accumulation & Zonal Statistics</b><br><sub>05_Hourly_Rainfall_Accumulation_and_Zonal_Statistics.ipynb</sub></td>
<td>สะสม rainfall rate ตามเวลาจริงของแต่ละ radar volume และสรุปปริมาณฝนด้วยเขตการปกครอง</td>
<td>Temporal integration, scan interval, event-centered accumulation, coverage, zonal statistics, rainfall volume</td>
<td>สะสมฝนจาก time-varying scans ได้, จัดการ temporal coverage ได้, คำนวณ ADM1/ADM2 zonal statistics และประเมิน uncertainty จาก Z–R relation ได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/05_Hourly_Rainfall_Accumulation_and_Zonal_Statistics.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/05_Hourly_Rainfall_Accumulation_and_Zonal_Statistics.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>06</b></td>
<td><b>Vertical Storm Structure, Cross-Section & Echo Top</b><br><sub>06_Vertical_Storm_Structure_CrossSection_and_EchoTop.ipynb</sub></td>
<td>วิเคราะห์โครงสร้างแนวดิ่งของพายุจาก pseudo-RHI, native radar gates และ Cartesian cross-section</td>
<td>Pseudo-RHI, vertical cross-section, echo base, echo depth, ET20/30/40/50, beam sampling, vertical reference</td>
<td>สร้าง cross-section ได้, อ่านโครงสร้างแนวดิ่งได้, คำนวณ echo-top thresholds ได้ และอธิบายข้อแตกต่างระหว่าง pseudo-RHI กับ gridded cross-section ได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/06_Vertical_Storm_Structure_CrossSection_and_EchoTop.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/06_Vertical_Storm_Structure_CrossSection_and_EchoTop.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>07</b></td>
<td><b>Echo Top, VIL, VILD & Severe-Storm Core Metrics</b><br><sub>07_EchoTop_VIL_VILD_and_SevereStorm_Core_Metrics.ipynb</sub></td>
<td>พัฒนา severe-storm diagnostics จาก 3-D reflectivity และติดตาม lifecycle ของ storm core ตลอดเหตุการณ์</td>
<td>Echo tops, composite ZH, height of max ZH, VIL, VILD, connected components, echo volume, lifecycle</td>
<td>คำนวณ ET40/ET50, VIL/VILD, severe-core area และ echo volume ได้, ระบุ storm core ได้ และติดตามการเปลี่ยนแปลงตามเวลาได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/07_EchoTop_VIL_VILD_and_SevereStorm_Core_Metrics.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/07_EchoTop_VIL_VILD_and_SevereStorm_Core_Metrics.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>08</b></td>
<td><b>Hail Detection, SHI, MESH & pyhail</b><br><sub>08_Hail_SHI_MESH_and_pyhail.ipynb</sub></td>
<td>คำนวณ hail-related radar retrievals โดยใช้ SHI/MESH/POSH ร่วมกับ thermal levels จาก observed remote sounding proxy</td>
<td>SHI, MESH, POSH, hail kinetic energy, 0°C/−20°C levels, pyhail, proxy sounding, thermal sensitivity</td>
<td>derive thermal levels จาก sounding ได้, คำนวณ SHI/MESH/POSH ได้, เปรียบเทียบ MESH formulations ได้ และอภิปราย uncertainty ของ proxy sounding ได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/08_Hail_SHI_MESH_and_pyhail.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/08_Hail_SHI_MESH_and_pyhail.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>09A</b></td>
<td><b>Integrated Severe-Storm & Hail Event Analysis</b><br><sub>09A_Integrated_SevereStorm_Hail_Event_Analysis.ipynb</sub></td>
<td>รวม severe-storm metrics และ hail retrievals เพื่อสร้าง event-scale physical interpretation โดยไม่คำนวณผลิตภัณฑ์เดิมซ้ำ</td>
<td>Integrated lifecycle, peak timing, peak lag, normalization, exploratory Spearman correlation, spatial synthesis</td>
<td>สร้าง integrated lifecycle ได้, เปรียบเทียบ peak timing ได้, วิเคราะห์ association แบบ exploratory ได้ และแยก fact, association และ causal interpretation ได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/09A_Integrated_SevereStorm_Hail_Event_Analysis.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/09A_Integrated_SevereStorm_Hail_Event_Analysis.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr><tr>
<td><b>10A</b></td>
<td><b>GIS Exposure & Administrative Analysis</b><br><sub>10A_GIS_Exposure_and_Administrative_Analysis.ipynb</sub></td>
<td>เชื่อม radar-derived severe/hail products กับ ADM1/ADM2 เพื่อวิเคราะห์ administrative exposure และ storm-core track</td>
<td>Raster–polygon overlay, zonal statistics, pixel-center vs all-touched, coverage filter, administrative ranking, storm track</td>
<td>ทำ GIS exposure analysis ได้, จัดอันดับหน่วยการปกครองโดยมี coverage control ได้, วิเคราะห์ storm-track intersection ได้ และแยก exposure ออกจาก verified impact ได้</td>
<td><a href="https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/10A_GIS_Exposure_and_Administrative_Analysis.ipynb">GitHub</a><br>
<a href="https://colab.research.google.com/github/nattaponm/Teaching_DRRAA_WeatherRadar_GIS/blob/main/10A_GIS_Exposure_and_Administrative_Analysis.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"></a></td>
</tr>
</tbody>
</table>

> หากชื่อไฟล์ Notebook 01 หรือ 02 ใน repository ถูกเปลี่ยนจากชื่อที่แสดงใน README ให้แก้ path ในปุ่ม Colab ให้ตรงกับชื่อไฟล์จริงบน branch `main`

---

## Concept map by notebook

### 01 — Radar & GIS Data Audit

เริ่มจากการทำความเข้าใจว่า radar file เป็น **volumetric observation** ไม่ใช่ภาพ 2-D ธรรมดา

```text
Volume
 ├── Sweep
 │    ├── Ray
 │    │    └── Gate
```

ผู้เรียนตรวจ metadata, time reference, field availability, elevation angles และโครงสร้าง GIS ก่อนการวิเคราะห์ทุกขั้น

**Key idea:** *Data understanding must precede data processing.*

### 02 — PPI, beam geometry and Doppler

PPI แสดงข้อมูลตามมุมกวาดของเสาอากาศ ณ elevation angle หนึ่ง

Radar beam height เพิ่มขึ้นตาม range และ elevation angle ดังนั้นสิ่งที่เรดาร์ “เห็น” ที่ระยะไกลอยู่สูงจากพื้นมากขึ้น

Doppler velocity เป็นเพียงองค์ประกอบความเร็วตามแนวลำแสง:

```text
Vr = component of wind / target motion along radar beam
```

**Key idea:** *Radial velocity is not the full wind vector.*

### 03 — Cartesian grid and CAPPI

Radar observation มี geometry แบบ polar แต่ GIS ส่วนใหญ่ทำงานใน Cartesian/projected coordinates

```text
Polar radar gates
      ↓ interpolation
3-D Cartesian grid
      ↓
CAPPI / raster / GIS
```

CAPPI จึงเป็น **interpolated spatial representation** ไม่ใช่ original measurement

**Key idea:** *Grid spacing is a numerical sampling choice, not observational resolution.*

### 04 — Z–R quantitative precipitation estimation

Reflectivity factor:

```text
Z = a R^b
```

ใช้แปลง radar reflectivity ไปเป็น rainfall rate

แต่ coefficient `a` และ `b` ขึ้นกับ microphysics และ storm regime จึงเปรียบเทียบหลาย Z–R relations เพื่อศึกษาความไวของ QPE

**Key idea:** *Radar-derived rainfall is an estimate, not ground truth.*

### 05 — Temporal accumulation and zonal statistics

Rainfall accumulation ต้อง integrate **rainfall rate × time support**

```text
P = Σ Ri Δti
```

ไม่ใช่การ sum dBZ

บทนี้ยังสอน radar coverage, NoData และการสรุปฝนใน polygon

**Key idea:** *Temporal support and spatial support are part of the measurement.*

### 06 — Vertical storm structure

พายุรุนแรงไม่สามารถอธิบายด้วย lowest-elevation PPI เพียงอย่างเดียว

บทนี้ใช้ pseudo-RHI และ Cartesian cross-section วิเคราะห์:

```text
echo base
echo depth
strong-reflectivity core
ET20 / ET30 / ET40 / ET50
```

**Key idea:** *Vertical extension of strong reflectivity provides information different from surface/low-level intensity.*

### 07 — Echo tops, VIL, VILD and severe-core metrics

บทนี้เปลี่ยน 3-D reflectivity volume เป็น storm-structure diagnostics

VIL ประมาณ vertically integrated reflectivity-derived liquid/ice loading proxy และ VILD normalize VIL ด้วย storm depth

```text
3-D ZH
 ↓
Echo top
VIL
VILD
40/50-dBZ core area
3-D echo volume
```

**Key idea:** *These are radar diagnostics, not direct measurements of hail mass or damage.*

### 08 — SHI, MESH and hail analysis

Severe Hail Index ใช้ reflectivity ร่วมกับ thermal weighting ระหว่าง freezing level และ −20°C level

```text
3-D reflectivity
      +
0°C / −20°C levels
      ↓
SHI
      ↓
MESH / POSH
```

Notebook เปรียบเทียบ MESH formulations และทำ thermal-level sensitivity

**Key idea:** *MESH is a radar-derived estimate of hail-size potential, not a measured hailstone diameter.*

### 09A — Integrated event analysis

รวมผลจาก severe-storm diagnostics และ hail retrievals โดยไม่คำนวณ algorithm เดิมซ้ำ

ศึกษา:

```text
peak timing
peak order
peak lag
normalized lifecycle
ET50–VIL–MESH association
```

Correlation ใช้เป็น exploratory analysis เนื่องจากมีเพียงประมาณ 10 scans

**Key idea:** *Association and timing differences do not establish causality.*

### 10A — GIS exposure and administrative analysis

เชื่อม radar-derived products กับ ADM1/ADM2:

```text
Radar raster
   +
Administrative polygon
   ↓
Zonal statistics
   ↓
Administrative exposure
```

วิเคราะห์ MESH, ET50, VIL และ storm-core track พร้อมเปรียบเทียบ pixel-center กับ `all_touched`

**Key idea:** *Administrative exposure is GIS overlap, not verified impact.*

---

## Recommended way to study

แนะนำให้เรียนตามลำดับ 01 → 10A เพราะแต่ละ Notebook ใช้ outputs และ concepts จากบทก่อนหน้า

### Undergraduate Year 3–4

ควรเน้น:

```text
01 → 02 → 03 → 04 → 05
              ↓
             06 → 07
              ↓
             09A → 10A
```

เป้าหมายหลักคือเข้าใจ radar/GIS workflow และตีความข้อมูลอย่างถูกต้อง

### Master’s level

ควรรันทุกบท รวมถึง:

- QPE sensitivity
- vertical storm structure
- severe-core lifecycle
- MESH formulation sensitivity
- proxy-sounding uncertainty
- exploratory statistics
- GIS rasterization sensitivity
- reproducibility metadata

---

## Quick start

1. Sign in to a Google account.
2. Open Notebook 01 using the **Open in Colab** button.
3. Mount Google Drive when requested.
4. Run all cells from top to bottom.
5. Allow Notebook 01 to create the common course workspace.
6. Continue in numerical order.
7. Do not skip readiness checks at the end of each notebook.
8. Review generated CSV, GeoTIFF, NetCDF, GeoPackage and figure outputs before moving to the next notebook.

Typical workspace created in Google Drive:

```text
Teaching_DRRAA_WeatherRadar_GIS/
├── 00_config/
├── 00_source_github/
├── 01_data/
│   └── gis/
└── events/
    └── 20230318_observed_hail_1106_1200/
        ├── 00_source_github/
        ├── 01_data/
        ├── 02_metadata/
        ├── 03_output/
        │   ├── csv/
        │   ├── geotiff/
        │   ├── netcdf/
        │   └── geopackage/
        ├── 04_figures/
        └── 99_logs/
```

---

## Reproducibility

แบบเรียนถูกออกแบบให้รักษา provenance ของการประมวลผลผ่าน:

- course configuration
- event-specific workspace
- readiness tables
- processing metadata
- figure manifests
- GeoTIFF metadata
- thermal-input provenance
- algorithm/version information

ผู้เรียนควรรักษาไฟล์เหล่านี้ไว้พร้อมผลการวิเคราะห์ ไม่ควรเก็บเฉพาะรูปภาพสุดท้าย

---

## Scientific interpretation rules

ก่อนใช้ผลจาก repository นี้ในรายงานหรือบทความ ควรแยกคำต่อไปนี้ออกจากกัน:

| Term | Meaning |
|---|---|
| **Observation** | สิ่งที่เครื่องมือวัดโดยตรง |
| **Processed field** | ข้อมูลที่ผ่าน QC/correction |
| **Interpolation** | ค่าที่สร้างบน spatial grid จาก observations |
| **Retrieval** | ตัวแปรที่คำนวณจาก observation ด้วย algorithm/assumption |
| **Exposure** | spatial overlap ระหว่าง hazard signature กับพื้นที่ |
| **Validation** | การเปรียบเทียบกับ independent observation |
| **Interpretation** | คำอธิบายเชิงกายภาพจากหลักฐานทั้งหมด |

ตัวอย่าง:

```text
70 dBZ
→ strong radar reflectivity

ET50 = 12 km MSL
→ 50-dBZ echo extends to 12 km MSL

MESH = 40 mm
→ radar-derived MESH estimate of 40 mm

ADM2 MESH ≥ 40 mm
→ administrative polygon overlaps pixels
   where radar-derived MESH ≥40 mm
```

ข้อความเหล่านี้ **ไม่เท่ากับ** การยืนยันลูกเห็บจริงขนาด 40 mm ในทุก pixel หรือทุกพื้นที่ของอำเภอ

---

## Outputs

ตลอดหลักสูตร ผู้เรียนจะได้ทำงานกับ scientific outputs หลายรูปแบบ:

```text
CSV        → metadata / statistics / lifecycle
PNG        → figures
NetCDF     → 3-D Cartesian radar grids
GeoTIFF    → GIS-ready radar products
GeoPackage → administrative exposure and storm track
```

Figures ถูกออกแบบให้ใช้ข้อความภาษาอังกฤษและความละเอียดประมาณ 300 dpi เพื่อให้นำไปต่อยอดงานวิจัยหรือ publication workflow ได้ง่าย

---

## Suggested student mini-projects

เมื่อเรียนถึง 10A สามารถต่อยอดได้ เช่น:

1. **Storm lifecycle** — เปรียบเทียบ Max ZH, ET50, VIL และ MESH
2. **QPE sensitivity** — เปรียบเทียบผลจาก Z–R relations
3. **Vertical storm structure** — วิเคราะห์ strong-reflectivity core
4. **Hail retrieval sensitivity** — เปรียบเทียบ MESH formulations
5. **Thermal uncertainty** — ศึกษาผลของ 0°C / −20°C levels ต่อ MESH
6. **Administrative exposure** — เปรียบเทียบ ADM1/ADM2 จาก ET50, VIL และ MESH
7. **Storm-track analysis** — วิเคราะห์เส้นทาง storm-core centroid กับ GIS
8. **Methodological uncertainty** — pixel-center vs all-touched zonal statistics

---

## Limitations of the current teaching case

กรณีศึกษานี้มีข้อจำกัดที่ต้องคำนึงถึง:

- เป็นเหตุการณ์ลูกเห็บกรณีเดียว
- event lifecycle มี radar volumes จำนวนจำกัด
- sounding เป็น remote observed proxy ไม่ใช่ local storm sounding
- MESH ยังไม่ได้ local calibration สำหรับประเทศไทย
- ไม่มี pixel-level observed hail-size validation
- ADM2 boundary เป็น simplified dataset
- GIS exposure ไม่ใช่ damage assessment
- statistical relationships ภายในหนึ่ง event เป็น exploratory
- severe-weather thresholds จากต่างประเทศไม่ควรนำมาใช้กับประเทศไทยโดยไม่ตรวจสอบ

---

## Data and software acknowledgment

แบบเรียนนี้ใช้แนวคิดและเครื่องมือจากชุมชน open-source atmospheric science และ geospatial science รวมถึง Py-ART, pyhail, GeoPandas, Rasterio, Shapely, PyProj, NumPy, Pandas, SciPy และ Matplotlib

ข้อมูลขอบเขตการปกครองมาจาก **geoBoundaries** ภายใต้ gbOpen / CC BY 4.0

ข้อมูล radar และ meteorological observations ควรได้รับการอ้างอิงตามหน่วยงานเจ้าของข้อมูลและเงื่อนไขการใช้งานของแหล่งข้อมูลต้นฉบับเมื่อถูกนำไปใช้ในงานวิจัยหรือการเผยแพร่

---

## Citation / use in teaching

หากนำ repository นี้ไปใช้ในการเรียนการสอน การอบรม หรือพัฒนางานวิจัยต่อ ขอแนะนำให้อ้างอิง:

```text
Teaching DRRAA Weather Radar & GIS
Weather-radar, severe-storm, hail and GIS analysis with Python / Google Colab
Repository: https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS
```

ควรอ้างอิง software และ original data sources ที่เกี่ยวข้องเพิ่มเติมตามงานที่นำไปใช้

---

## Repository

https://github.com/nattaponm/Teaching_DRRAA_WeatherRadar_GIS

---

### Final message

เป้าหมายของ repository นี้ไม่ใช่เพียงให้ผู้เรียน “รันโค้ดได้” แต่ให้สามารถตอบได้ว่า:

> **What was measured?  
> What was processed?  
> What assumptions were introduced?  
> What does the resulting product physically mean?  
> And what can — or cannot — be concluded from it?**
