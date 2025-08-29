## TerriaMap for the Hunga Tonga Case Study

One of the key challenges in the Hunga Tonga study was to make geographic exploration **visual, intuitive, and interdisciplinary**. To address this, the team set up and customized **TerriaMap**, an open-source web application designed to integrate and visualize diverse geospatial datasets within a single interactive dashboard.

A tailored TerriaMap instance was deployed on the **FAIR-EASE** infrastructure hosted by *Université de Clermont Auvergne*. This setup allowed participants to visualize and interact with a wide range of datasets, including:

- **Volcanic and seismic activity**: magnitude, depth, and location in the time period around the eruption.
- **Satellite data on the volcanic plume**, including SO₂ emissions.
- **Satellite ocean colour data** for tracking changes in surface waters.
- **In situ physical and biogeochemical ocean data** from ARGO floats.
- **Biological and omics datasets**, with dynamic links to external repositories such as the [European Nucleotide Archive (ENA)](https://www.ebi.ac.uk/ena).
- **Bathymetric maps** and other environmental layers.

Dynamic feature info templates were configured to provide context and direct access to related resources. The integration was further enhanced by enabling **TerriaMap to be launched directly from within Galaxy** through a dedicated interactive tool, making geospatial exploration accessible alongside analytical workflows.

TerriaMap’s **open-source nature** and support for a wide variety of data formats and services (WMS, ERDDAP, CSV, COG, etc.) made it an ideal platform for cross-disciplinary data integration. Its flexibility opens possibilities for future enhancements, such as improved support for:
- **ERDDAP data services**
- **OGC SensorThings API**
- **RO-Crates**
- **SpatioTemporal Asset Catalog (STAC)** items and catalog groups

The **Data Stories** functionality—an interactive narrative mode that can guide users through curated datasets—was identified as a particularly promising feature. For the Hunga Tonga case, it could be used to build a **timeline-based story** showing the sequence of events and data layers of interest, from the first seismic activity to post-eruption biological changes.

Although time constraints during the Hackathon limited exploration of all of TerriaMap’s capabilities, the experience demonstrated its strong potential for:
- **Cross-disciplinary integration** of FAIR-EASE use case datasets.
- Serving as a **powerful, browser-based dashboard** for environmental research.
- **Curating and publishing** complex geospatial datasets in an accessible and visually engaging way.

In the context of Hunga Tonga, TerriaMap provides a means to **connect atmospheric, oceanographic, geochemical, and biological data** into a single, intuitive interface—allowing researchers to explore correlations, identify patterns, and better understand the event’s impact across multiple environmental domains.
