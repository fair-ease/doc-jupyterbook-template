## 1.2. How did we proceed ?

The initial phase of the study consisted in identifying datasets that could provide meaningful insights into the potential phytoplankton response following the Hunga Tonga eruption (see Annex: Data Inventory). This exploratory step aimed to compile a comprehensive list of relevant satellite, in situ, and biogeochemical data sources. While the Data Inventory includes all datasets considered during this phase, not all were ultimately retained for analysis. The selection was refined based on data quality, coverage, relevance to the research questions, and technical feasibility. The list below details the datasets that were effectively accessed, processed, and used in the present study.

### Datasets Utilized

#### Satellite Ocean Colour Data (Copernicus Marine Service – GlobColour)
We used daily Level-3 products providing:
- Chlorophyll-a concentrations from the multi-sensor plankton dataset (`cmems_obs-oc_glo_bgc-plankton_my_l3-multi-4km_P1D`), used as a proxy for phytoplankton biomass.
- Particulate backscattering coefficients (BBP) from the multi-sensor optics dataset (`cmems_obs-oc_glo_bgc-optics_my_l3-multi-4km_P1D`), serving as an indicator of suspended particle concentrations in the upper ocean, including potential ash deposition.  

Access: **Copernicus Marine Service**

#### MODIS-Aqua Fluorescence Data (NASA)
- Level-2 nFLH (Normalized Fluorescence Line Height) products from the MODIS instrument onboard the Aqua satellite were used to assess chlorophyll fluorescence under the satellite track.
- These data, available at high temporal resolution, are ungridded and required custom preprocessing due to their atypical NetCDF format.  

Access was limited by download constraints and temporal gaps.  
Access: **NASA Earthdata**

#### BGC-Argo Float Data (Euro-Argo / Ifremer)
Biogeochemical Argo data were sourced from the global Argo database. Two floats (WMO 6903024 and 6903025), located approximately 700 km from the eruption site, were equipped with Seabird ECO triplet sensors measuring:
- Chlorophyll-a (via in situ fluorescence)
- BBP at 700 nm  

Access: **Argo DOI**  
webODV Access: https://webodv-egi-ace.cloud.ba.infn.it/login

#### GEOTRACES – Discrete Seawater Samples (IDP2021v2)
The GEOTRACES IDP2021 database provided key geochemical tracers, such as dissolved iron (Fe) as well as rare earth elements (RRE):  
Dataset: `GEOTRACES_IDP2021_Seawater_Discrete_Sample_Data_v2`  

Access: **BODC Repository**  
webODV Access: https://explore.webodv.awi.de/ocean/tracer/geotraces/idp2021/seawater

#### Global tritium and helium isotope data compilation of Jenkins et al., 2019
A comprehensive global oceanic dataset of helium isotope and tritium measurements.  
webODV Access: https://explore.webodv.awi.de/ocean/tracer/tritium-helium/jenkins-etal-2019

#### Sea Surface Currents and Absolute Dynamic Topography (ADT)
Sea Surface Height measured by altimetry and derived variables (geostrophic velocities). Daily Level-4 data products were used to visualize surface circulation and sea surface height anomalies:
- Derived from the DUACS multi-satellite altimetry product  
- Dataset: `cmems_obs-sl_glo_phy-ssh_my_allsat-l4-duacs-0.125deg_P1D`  

Access: **Copernicus Sea Level Product**  
webODV Access: https://webodv.eoscfe.mesocentre.uca.fr/ocean/satellite/ssh/cmems_obs-sl_glo_phy-ssh_my_allsat-l4-duacs-0.125deg_p1d_1740757825231/

#### Atmospheric Data on the volcanic plume composition in gas (SO₂) and particles
High-frequency geostationary and low-earth orbit satellite data were employed to track volcanic emissions:

- **HIMAWARI-8/AHI (GEO)**: Provided RGB composite images for tracking particles (including ash, sulfate aerosols, ice crystals, etc…) with high temporal resolution.
- **Sentinel-5P / TROPOMI (LEO)**: Offered SO₂ gas plume detection and tracking over longer time periods.

These datasets were accessed and visualized through the **VolcPlume** platform: https://volcplume.aeris-data.fr/

**Data Access Notes:**
- HIMAWARI-8 RGB composites: *Composites*
- Raw HIMAWARI-8 L1 data: *Raw Data*
- Sentinel-5P SO₂ L2 products: *TROPOMI Data*  
  *(Note: ORCID or ICARE credentials are required for access.)*  
  Reference: Boichu et al., 2023 – DOI

#### Etna Case Study – Volcanic Activity Metadata
To support comparative analysis, data on Etna’s ash emission events were retrieved from the **VONA** (Volcano Observatory Notices for Aviation) database, managed by INGV. These records provided:
- Eruption dates
- Ash plume directions during paroxysmal events  

Access: **INGV VONA**

---