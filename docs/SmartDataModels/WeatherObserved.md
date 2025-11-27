
The **WeatherObserved** Smart Data Model is used to represent real-time meteorological observations within the **PGTEC** project.  
It follows the official FIWARE definition and does not require any structural modification, ensuring full compatibility and interoperability with other FIWARE-based systems.

This model serves as the standard framework for integrating **real-time data** collected from multiple external sources, including:

- :material-earth: [**AEMET**](https://www.aemet.es/es/portada) — Agencia Estatal de Meteorología
- :droplet: [**CHJ**](https://www.chj.es/es-es/Paginas/Home.aspx) — Confederación Hidrográfica del Júcar 
- :cloud: [**AVAMET**](https://www.avamet.org/) — Agencia Valenciana de Meteorología
- :thunder: [**SiAR**](https://servicio.mapa.gob.es/websiar/) — Sistema de información agroclimática para el regadío

By adopting the *WeatherObserved* schema, all incoming data are harmonized under a **common structure**, ensuring consistency in variable names, measurement units, and metadata representation across the entire data ecosystem.

---

### Main Variables of Interest

The following table describes the most important variables used in the PGTEC project:

| **Description** | **FIWARE Attribute** | **Unit** |
|:------------------------------------|:--------------------:|:--------------------|
| Precipitation                       | `precipitation`      | mm, l/m²            |
| Air temperature                     | `temperature`        | °C                  |
| Relative humidity                   | `relativeHumidity`   | %                   |
| Snow depth                          | `snowHeight`         | mm                  |
| Wind speed                          | `windSpeed`          | m/s, km/h           |

---

### Role within PGTEC

Within **PGTEC**, the *WeatherObserved* model is primarily used for the ingestion of **real-time meteorological data**. This approach ensures a unified and interoperable data layer, allowing seamless integration between the **Airflow pipelines**, **FastAPI services**, and the **TETIS dashboard**, where users can visualize or request the latest standardized weather observations.
