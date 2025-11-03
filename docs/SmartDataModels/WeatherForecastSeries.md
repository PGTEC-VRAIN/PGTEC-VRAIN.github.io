
The **WeatherForecastSeries** Smart Data Model is an **extension of the official** [WeatherForecast](https://smart-data-models.github.io/dataModel.Weather/WeatherForecast/schema.json) model from FIWARE’s Smart Data Models initiative.  
Its main goal is to enable the representation of **forecast time series** (rather than a single prediction) within a single entity.

---

### 🔄 Key Modifications

- **Array-based attributes**  
  Most of the variable types defined in the original `WeatherForecast` model have been converted into **arrays of their base type**.  
  This structure allows the model to store **multiple forecasted values** (e.g., temperature, wind speed, precipitation) corresponding to **different timestamps** within a single object.

- **Inlined definitions**  
  Some variables originally referenced from [Weather-Commons](https://smart-data-models.github.io/dataModel.Weather/weather-schema.json#/definitions/Weather-Commons) have now been defined **directly inside the WeatherForecastSeries schema**, improving self-containment and making the model easier to use independently.

- **New `timestamps` attribute**  
  A new property, `timestamps`, has been introduced to specify the **exact prediction times** corresponding to each value in the variable arrays.  
  This makes it possible to directly associate each forecasted parameter with its valid time, simplifying temporal analysis.

---

### 🌦️ Purpose and Advantages

This model enables the aggregation of **complete forecast time series** (e.g., hourly or daily predictions) in a **single JSON object**, reducing redundancy and improving data retrieval efficiency.

In the **PGTEC project**, it is used to:

- Store **weather predictions** retrieved from different data sources such as AEMET, Open-Meteo, and Copernicus.  
- Provide these standardized forecasts as input for the **TETIS hydrological model**, ensuring that all variables share a common format and temporal alignment.  
- Facilitate **interoperability** between APIs, Airflow workflows, and visualization dashboards.

---

### 🧩 Example Entity

Below is an example of a `WeatherForecastSeries` entity representing 3-hourly weather predictions for a given location:

```json
{
  "id": "WeatherForecastSeries:Valencia:2025-03-01",
  "type": "WeatherForecastSeries",
  "location": {
    "type": "Point",
    "coordinates": [-0.3763, 39.4699]
  },
  "timestamps": [
    "2025-03-01T00:00:00Z",
    "2025-03-01T03:00:00Z",
    "2025-03-01T06:00:00Z"
  ],
  "temperature": [14.5, 13.8, 13.1],
  "precipitation": [0.0, 0.2, 1.1],
  "windSpeed": [3.4, 2.8, 4.1],
  "relativeHumidity": [65, 70, 72],
  "source": "AEMET",
  "address": {
    "addressLocality": "Valencia",
    "addressCountry": "ES"
  },
  "dateIssued": "2025-03-01T00:00:00Z",
  "validFrom": "2025-03-01T00:00:00Z",
  "validTo": "2025-03-01T06:00:00Z"
}
