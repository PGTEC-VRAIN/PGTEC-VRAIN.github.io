---
icon: material/puzzle-outline
title: Smart Data Models
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

## Overview

The **Smart Data Models** initiative, led by FIWARE Foundation, provides a set of open and interoperable data models designed to promote common standards for data exchange. These models define the structure, semantics, and units of measurement for key environmental and urban variables, allowing data to be easily reused and understood across multiple platforms and applications.

Within the PGTEC project, the adoption of Smart Data Models plays a key role in ensuring that data collected from diverse environmental and meteorological sources can be seamlessly integrated and understood. The project aims to harmonize and translate heterogeneous datasets—originating from different agencies and monitoring systems—into a unified, standardized format that facilitates interoperability, data sharing, and contextual analysis. By using standardized FIWARE-based schemas, the project ensures that variables—such as temperature, precipitation, or relative hummidity, among others, are represented consistently, regardless of their origin. This harmonization makes easier the training of the TETIS hydrological model using different data sources such as Open-Meteo or AEMET. It also enables more accurate analysis and improved decision-making.

### Smart Data Models for PGTEC

To achieve this, PGTEC implements and extends several Smart Data Models tailored to the project’s specific needs. The main models used include *WeatherObserved*, which harmonizes **meteorological real time data** from different meteorological agencies; WeatherForecastSeries, an extended version of the FIWARE WeatherForecast model adapted to handle **meteorological predictions**; and *StreamFlow*, a new model specifically designed to represent *hydrological variables* such as flow and gauging data from the Confederación Hidrográfica del Júcar (CHJ).

As mention above, three different Smart Data Models have been designed, each focused on a specific type of data source. These include real-time data sources, climate model forecast sources, and hydrological data sources.

- **[WeatherObserved](WeatherObserved.md):** Fiware smart data model used to translate all the real time data. For more information about the model go to the [json schema](https://github.com/smart-data-models/dataModel.Weather/blob/master/WeatherObserved/schema.json). This model will be used in different climate data sources such as:

  - AEMET: Agencia Estatal de Meteorología
  - CHJ: Confederación Hidrográfrica del Júcar
  - SiAR: Sistema de Información Agroclimática para el regadío
  - AVAMET: Agencia Estatal de Meteorología

- **[WeatherForecastSeries](WeatherForecastSeries.md):**. An extension of the smart data model [WeatherForecast](https://github.com/smart-data-models/dataModel.Weather/blob/master/WeatherForecast/schema.json) adaptad to time series data. Fore more information visit the [json schema](https://github.com/PGTEC-VRAIN/SmartFlow/blob/main/SmartFlowAPI/SmartDataModels/WeatherForcastSeries/schema.json).

- **[StreamFlow](StreamFlow.md):** A new Smart Data Model focused on CHJ hydrometeorological data. It standardizes variables such as gauging and flow rates into a consistent format using the FIWARE Smart Data Models ontology. For deep understanding of the structure, visit the [github](https://github.com/PGTEC-VRAIN/WorkflowPTGEC/blob/juan/tetis/hydrographic_models.py).

![Smart Data Models image](images/logo_smd.png){ width="400" style="display:block; margin:auto;" }
