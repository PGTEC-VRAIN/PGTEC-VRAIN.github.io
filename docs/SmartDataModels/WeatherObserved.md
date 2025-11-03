## :material-weather-partly-cloudy: SMART DATA MODEL – WeatherObserved

The **WeatherObserved** Smart Data Model is used to represent real-time meteorological observations within the **PGTEC** project.  
It follows the official FIWARE definition and does not require any structural modification, ensuring full compatibility and interoperability with other FIWARE-based systems.

This model serves as the standard framework for integrating **real-time data** collected from multiple external sources, including:

- :es: **AEMET** — Agencia Estatal de Meteorología
- :droplet: **CHJ** — Confederación Hidrográfica del Júcar 
- :cloud: **AVSRE** — Agencia Valenciana de Seguridad y Respuesta a las Emergencias  

By adopting the *WeatherObserved* schema, all incoming data are harmonized under a **common structure**, ensuring consistency in variable names, measurement units, and metadata representation across the entire data ecosystem.

---

### 📊 Variable Mapping

| **Variable (IIAMA)** | **Description**                      | **FIWARE Attribute** | **Unit**            |
|:----------------------|:------------------------------------|:--------------------:|:--------------------|
| **P**                 | Precipitation                       | `precipitation`      | mm, l/m²            |
| **T**                 | Air temperature                     | `temperature`        | °C                  |
| **Hum**               | Relative humidity                   | `relativeHumidity`   | %                   |
| **Ni**                | Snow depth                          | `snowHeight`         | mm                  |
| **Vviento**           | Wind speed                          | `windSpeed`          | m/s, km/h           |

> 💡 *All these attributes are already defined in the original FIWARE* `WeatherObserved` *schema and can be used directly to ingest data from sensors, observation stations, or open APIs.*

---

### 🌦️ Role within PGTEC

Within **PGTEC**, the *WeatherObserved* model is primarily used for the ingestion of **real-time meteorological data**, complementing:

- **WeatherForecastSeries** → for forecasted weather data  
- **StreamFlow** → for hydrological flow and discharge measurements  

This approach ensures a unified and interoperable data layer, allowing seamless integration between the **Airflow pipelines**, **FastAPI services**, and the **TETIS dashboard**, where users can visualize or request the latest standardized weather observations.
