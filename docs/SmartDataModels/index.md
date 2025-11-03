---
icon: material/puzzle-outline
title: Smart Data Models
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

# Overview

The **Smart Data Models** initiative, led by FIWARE Foundation, provides a set of open and interoperable data models designed to promote common standards for data exchange. These models define the structure, semantics, and units of measurement for key environmental and urban variables, allowing data to be easily reused and understood across multiple platforms and applications.

Within the PGTEC project, the adoption of Smart Data Models plays a key role in ensuring that data collected from diverse environmental and meteorological sources can be seamlessly integrated and understood. The project aims to harmonize and translate heterogeneous datasets—originating from different agencies and monitoring systems—into a unified, standardized format that facilitates interoperability, data sharing, and contextual analysis. By using standardized FIWARE-based schemas, the project ensures that variables—such as temperature, precipitation, or relative hummidity, among others, are represented consistently, regardless of their origin. This harmonization enables more accurate analysis, improved decision-making, and better collaboration between weather institutions like AEMET, CHJ, and AVSRE.

To achieve this, PGTEC implements and extends several Smart Data Models tailored to the project’s specific needs. The main models used include WeatherObserved, which harmonizes observational data from different meteorological agencies; WeatherForecastSeries, an extended version of the FIWARE WeatherForecast model adapted to handle forecast time series; and CHJ, a new model specifically designed to represent hydrological variables such as flow and gauging data from the Confederación Hidrográfica del Júcar (CHJ).

## Smart Data Models proposed

Para el proyecto, se ha pensado en tener 3 Smart Data Models diferentes enfocados cada uno en un tipo de fuente de datos. Hay fuentes de datos en tiempo real, fuentes de datos que resultan ser predicciones de modelos climáticos y fuentes de datos hidrológicas 

- **[WeatherObserved](https://fiware-datamodels.readthedocs.io/en/stable/Weather/WeatherObserved/doc/spec/index.html):** Fiware smart data model used to translate all the data from different climate data sources such as:
    - AEMET: Agencia Española de Meteorología
    - CHJ: Confederación Hidrográfrica del Júcar
    - AVSRE: Agencia Valenciana de Seguridad y Respuesta a emergencias

- **[WeatherForecastSeries](https://github.com/PGTEC-VRAIN/SmartFlow/blob/main/SmartDataModels/WeatherForcastSeries/schema.json):**. An extension of the smart data model [WeatherForecast](https://fiware-datamodels.readthedocs.io/en/stable/Weather/WeatherForecast/doc/spec/index.html)

- **[StreamFlow](https://github.com/PGTEC-VRAIN/WorkflowPTGEC/blob/juan/tetis/hydrographic_models.py):** A new Smart Data Model focused on CHJ hydrometeorological data. It standardizes variables such as gauging and flow rates into a consistent format using the FIWARE Smart Data Models ontology.


![Smart Data Models image](images/logo_smd.png){ width="400" style="display:block; margin:auto;" }
