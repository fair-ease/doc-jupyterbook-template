# Annex

## Data Inventory

### Time period
20th of November – 30th January (climax on the 15th of January 2022)

### Geographic Bounding Box
- **north**: -17.634  
- **east**: 187.927  
- **south**: -22.958  
- **west**: 182.269  

---

## Satellite Data (Atmospheric & Oceanic)

### Volcanic Plume & Gas Tracking

#### HIMAWARI-8 (GEO)
- Tracks volcanic ash, sulfate aerosols, ice crystals.  
- Best time resolution for dispersion analysis.  
- Data can be visualised with the **VolcPlume** web platform: [https://volcplume.aeris-data.fr/](https://volcplume.aeris-data.fr/)  
- GeostatRGB composites for the relevant region and dates: [link](https://www.icare.univ-lille.fr/login/?prourl=/asd-content/archive/?dir=GEO/HIMAWARI+1407/BROWSE-L1/2022/)  
- Raw data: [link](https://www.icare.univ-lille.fr/login/?prourl=/asd-content/archive/?dir=GEO/HIMAWARI+1407/L1_B/2022/) *(registration using ORCID or Icare ID)*  
- Relevant paper: Boichu et al. 2023 – [DOI](https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2023JD039010)

#### Sentinel-5P/TROPOMI (LEO)
- Tracks SO₂ gas emissions, which persist longer than ash.  
- Data can be visualised with the **VolcPlume** web platform: [https://volcplume.aeris-data.fr/](https://volcplume.aeris-data.fr/)  
- TROPOMI data: L2 products (files labelled SO2) for 2022 are available [here](https://www.icare.univ-lille.fr/login/?prourl=/asd-content/archive/?dir=S5P/L2.v02/2022/) *(registration using ORCID or Icare ID)*  
- Volcano Thredds: [https://thredds.icare.univ-lille.fr/thredds/catalog/catalog.xml](https://thredds.icare.univ-lille.fr/thredds/catalog/catalog.xml)  

---

### Ocean Color & Phytoplankton Blooms

#### Copernicus-GlobColour (CMEMS)
- **L3 (daily)** dataset (Bio-Geo-Chemical ocean color observations): [link](https://data.marine.copernicus.eu/product/OCEANCOLOUR_GLO_BGC_L3_MY_009_103/description)  
- **L4 (monthly interpolated)** dataset (multi-sensor combined). DOI for L4: [https://doi.org/10.48670/moi-00148](https://doi.org/10.48670/moi-00148)  
- **Daily L4**: [link](https://data.marine.copernicus.eu/product/OCEANCOLOUR_GLO_BGC_L4_MY_009_104/description)  
- Chlorophyll-a concentration (CHL) to track phytoplankton blooms: [DOI](https://doi.org/10.17882/102324)  
- Relevant paper: [Frontiers in Marine Science](https://www.frontiersin.org/journals/marine-science/articles/10.3389/fmars.2022.1028022/full)  

#### Sentinel-3A/B OLCI (Ocean Land Colour Instrument)
- Best sensor for detecting fluorescence (better phytoplankton tracking).  
- [EUMETSAT page](https://www.eumetsat.int/S3-OLCI-FLUO)  
- ESA browser: [link](https://browser.dataspace.copernicus.eu/?zoom=4&lat=-14.47723&lng=-179.73633&themeId=DEFAULT-THEME&visualizationUrl=U2FsdGVkX1%2Bfi6dTBSC7V%2FTC%2Fk13JfjwPvNsYdj6ys0F3jphrBYt1lHQCf%2ByuIrr23vHCc4C1o4ffrYqC88XnS%2F%2BypGnyvHPUNeRDoY8qh2fRNhQcS0hPIcg6wia9%2BbX&datasetId=S3OLCIL2_WATER&fromTime=2022-01-15T00%3A00%3A00.000Z&toTime=2022-01-15T23%3A59%3A59.999Z&layerId=2_WATER_CHL_OC4ME)  

#### MODIS Aqua data L2 *(to be confirmed)*
- Ordered from [NASA Earthdata](https://urs.earthdata.nasa.gov/) MODIS L2 data (1 Jan 2022 – 28 Feb 2022, 1GB) containing nFLH (Normalized Fluorescence Line Height). Not yet explored.

---

### CMEMS (Global Ocean Current Data)
- Provides continuous surface circulation data.  
- Daily altimetry product with calculated geostrophic currents.  
- **Global Ocean Gridded L4 Sea Surface Heights and Derived Variables**: [link](https://data.marine.copernicus.eu/product/SEALEVEL_GLO_PHY_L4_MY_008_047/description)  
- DOI: [https://doi.org/10.48670/moi-00148](https://doi.org/10.48670/moi-00148)  
- Possible to overlay with Argo float trajectories.

---

## Ocean Data (In Situ Measurements)

### Water Chemistry & Nutrients

#### GEOTRACES Data (IDP2021)
- Provides Iron and Silicate concentrations pre- and post-eruption.  
- Dataset: `GEOTRACES_IDP2021_Seawater_Discrete_Sample_Data_v2`  
- [BODC access](https://www.bodc.ac.uk/data/published_data_library/catalogue/10.5285/ff46f034-f47c-05f9-e053-6c86abc0dc7e/)  
- On webODV see with Reiner  

#### World Ocean Atlas (WOA)
- Climate Fields Data (temperature, salinity, dissolved nutrients).  
- THREDDS: [catalog](https://www.ncei.noaa.gov/thredds-ocean/catalog.html) | [WOA23 catalog](https://www.ncei.noaa.gov/thredds-ocean/catalog/woa23/DATA/catalog.html)  
- FTP: `ftp://ftp.nodc.noaa.gov/pub/data.nodc/`

---

### Argo Float Data (Biogeochemical & Physical)
- **BGC-Argo (Global Data Assembly Centre)**  
  - Key floats: 6903024 & 6903025 (located near eruption)  
  - Particle Backscattering (BBP) signals possibly linked to ash fallout  
  - Chlorophyll-a (CHL-a) concentration from Argo profiles  
  - Argopy tool in Galaxy: [link](https://earth-system.usegalaxy.eu/root?tool_id=toolshed.g2.bx.psu.edu/repos/ecology/argo_getdata/argo_getdata/0.1.15+galaxy0)  
- Access:
  - S3 bucket on AWS (Galaxy)
  - Direct NetCDF files from Argo GDAC
- **Beacon**: Franz et al. 2024 paper shows discrepancy between Argo data and satellite ocean color  
- **BGC-Argo Synthetic Profile Collection (Chlorophyll-A)**: [DOI](https://doi.org/10.17882/102324)  

---

### AVISO Maps (Surface Current & Float Positions)
- Historical datasets available.  
- Action: Catherine to clean and analyze this data.

---

### Ocean Biological Data
- Help of the bioinformatic team from Ifremer  
- NCBI – WWW Error Blocked Diagnostic  

---

## webODV Access Links of Relevant Datasets

### webODV Explore Server – FAIR-EASE Testbed
- `cmems_mod_med_bgc-plankton_my_4.2km_P1Y-m_1732549229584` – Chlorophyll (annual mean) | OCEANCOLOUR_MED_BGC_L3_MY_009_143 | 2016 – 2022  
- `MODIS-A_L3_mean_Chlo_2019-03-21_2019-06-21` – MODIS/Aqua Level-3 Chlorophyll Concentration, OCI Algorithm (2019-03-21 – 2019-06-21) – European Seas  
- `cmems_obs-oc_adriatic_bgc-plankton_my_l3-multi-1km` – Multi-sensor and multi water-type Chlorophyll a concentration | VIIRSJ JPSS-1 - Level2, VIIRSN Suomi-NPP - Level2 | Northern Adriatic | Nov 2015 – Nov 2019  
- `cmems_obs-oc_glo_bgc-plankton_my_l4-olci-300m_P1M_1740837458978` – Monthly GlobColour Chlorophyll-a concentration | Hunga Tonga region | Jan – Feb 20_
