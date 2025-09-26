---
icon: material/database
title: Information
hide:
  - toc
---

<script>
    // Hide sidebar. This script is only executed in the data sources page.
    document.addEventListener('DOMContentLoaded', function () {
        const sidebar = document.querySelector('.md-sidebar--secondary');
        if (document.querySelector('.catalog-header') && sidebar) {
            sidebar.style.display = 'none';
            sidebar.style.width = '0';
            sidebar.style.padding = '0';
            sidebar.style.margin = '0';
        }
    });
</script>


<div class="catalog-header" markdown>
<div markdown>
This section will detail the different data sources available to feed the prediction models and algorithms that will enable us to anticipate extreme weather events, thereby contributing to a more effective response to meteorological emergencies. Their usefulness, quality and availability will be evaluated.
</div>
</div>
## Data Sources

<div class="grid cards cols-3" markdown>

- :material-water-outline: **Conferencia Hidrográfica del Júcar – SAIH**

    Public body responsible for water management in the Júcar River Basin District.

    [:octicons-arrow-right-24: Learn more](./metadata_datasources/siah_datasource.md)

- :material-sprout-outline: **Sistema de Información Agroclimática para el Regadío (SiAR)**

    Network of over 520 weather stations that captures, records, and disseminates agroclimatic data necessary to determine the water demand of irrigated farms.

    [:octicons-arrow-right-24: Learn more](./metadata_datasources/siar_datasource.md)

- :material-weather-partly-cloudy: **Agencia Estatal de Meteorología (AEMET)**

    Official Spanish government agency responsible for observing, forecasting and studying meteorological phenomena.  

    [:octicons-arrow-right-24: Learn more](./metadata_datasources/aemet_datasource.md)

- :material-grid: **AEMET (ROCIO)**

    AEMET Observational Grid with Optimal Interpolation. 

    [:octicons-arrow-right-24: Learn more](./metadata_datasources/aemet_rocio_datasource.md)

- :material-chart-line: **AEMET (Spain02)**

    Institutional collaboration between AEMET and the Santander Meteorology Group (SMG) at the University of Cantabria-CSIC.  

    [:octicons-arrow-right-24: Learn more](./metadata_datasources/aemet_spain_datasource.md)

- :material-earth: **Copernicus**

    Project coordinated and managed by the European Commission.

    [:octicons-arrow-right-24: Learn more](./metadata_datasources/copernicus_datasource.md)

- :material-water-percent: **MSWEP**

    Multi-Source Weighted-Ensemble Precipitation (MSWEP) is a high-resolution global precipitation dataset.  

    [:octicons-arrow-right-24: Learn more](./metadata_datasources/mswep_datasource.md)

- :material-domain: **CEDEX**

    It is the centre for studies and experimentation in public works.

    [:octicons-arrow-right-24: Learn more](./metadata_datasources/cedex_datasource.md)

- :material-shield-account: **AVSRE**

    The Valencian Agency for Security and Emergency Response (AVSRE) manages civil protection, emergency management, firefighting and public safety in the Valencian Community.
    
    [:octicons-arrow-right-24: Learn more](./metadata_datasources/avsre_datasource.md)

</div>
