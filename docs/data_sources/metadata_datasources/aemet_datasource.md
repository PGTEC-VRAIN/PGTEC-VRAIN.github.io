# Agencia Estatal de Meteorología (AEMET)

**The State Meteorological Agency (AEMET)** is the official Spanish government body responsible for observing, predicting and studying meteorological phenomena. As the main authority, AEMET provides reliable, consistent and standardised data, following the guidelines of the World Meteorological Organisation (WMO). 

Its [AEMET OpenData](https://opendata.aemet.es/centrodedescargas/inicio) service is the designated platform for disseminating this information, offering access to a wide range of **meteorological** and **climatological** products. The quality of its data is backed by rigorous validation processes and by the National Plan for the Prediction and Monitoring of Adverse Meteorological Phenomena (Meteoalerta), which establishes the risk thresholds for alerts. 

In the **Valencian Community**, there are approximately **40 meteorological stations** that transmit data on a regular basis and are therefore used for live weather monitoring. 

It should be noted that, although **real-time data** is subject to automatic checks, it may contain occasional errors. Even so, the data collected by AEMET is considered to be of **high quality** due to its official nature. Consolidated climate data undergoes more exhaustive validation processes before its final publication. 


## API
The AEMET API is based on **REST architecture** and returns data mainly in **JSON** format, using international standards such as **CAP** (Common Alerting Protocol) for warnings and **GeoJSON** to represent affected areas.

Data is available on:

- Meteorological observations
- Weather forecasts
- Radar and lightning
- Alerts

With regard to **historical data**, there is no fixed start year for the data in the ‘climatological values’ section of the API. For daily, monthly and annual climatology and extreme values, the start date of the records depends on each individual weather station. For normal climatology, it returns average values calculated over the period from **1991** to **2020**. 

The API is **public**, but registration is required. An API Key must be requested on the official [AEMET OpenData](https://opendata.aemet.es/). It is valid for **three months** and is linked to an **email address**. 

<!-- ??? info "More information"
    The API has a [Swagger](https://opendata.aemet.es/dist/index.html) available, although it depends on **server availability**. There are recurring **instability issues** such as timeouts and intermittent unavailability. This lack of reliability presents a significant risk and requires the implementation of fault-tolerant architectures. 

    The data retrieval process takes place in **two steps**:

    - The first request returns **metadata** and a **download URL**.

    - The client must make a **second request** to that URL to finally obtain the **data**. 

    The service imposes **rate limits**, HTTP code 429 ‘Too Many Requests’, when the flow per minute is exceeded. For intensive use, it is advisable to coordinate with AEMET to avoid blockages. It has also been detected that when the link is generated and the server fails, when the link is accessed again, it sometimes returns 404 ‘Expired data’ because the link has expired. 
 -->
