---
title: Predictions 
---

## Overview

Different climate agencies around the world are used to provide weather forecast data from their climate models. In this case, the Open-Meteo wrapper is used, as it provides direct access to the forecasts of several climate models via an API, eliminating the need to navigate to the official websites of each climate agency individually. It also offers the data in a standardised format, facilitating conversion to the JSON-LD format used by Smart Data Models. The climate agencies that hold relevant PGTEC project predictions data, given their national scope, are:

- CNC (Canadian National Committee):  
    - Model GEPS (Global Ensemble Prediction System). 

- NOAA (National Oceanic and Atmospheric Administration):  
    - Model GFS (Global Forecasting System). 

- DWD (Deutscher Wetterdienst):  
    - Model ICON (Icosahedral Con-hidrostático). 

- Meteofrance:
    - Model Arpege-Arome. 

- ECMWF (Europe Centre for Medium Weather Forecasts): 

    - Model IFS (Integrated Forecasting System). 

    - Model AIFS (Artificial Intelligence Forecasting System). 

    - Model Seas5 (Seasonal Forecasting System 5). 

- AEMET (Agencia Estatal de Meteorología):  
    - Model Harmonie-Arome. 

The data flow for weather forecasts differs considerably from the [real-time data flow](../real_time_data_flow/index.md). Since weather forecasts provided by climate models cover time spans ranging from several days to weeks, storing all of these forecasts in Orion-LD and persisting them in TimeScaleDB would incur very high computational costs. Therefore, we have chosen to store the forecast files directly in Amazon S3 buckets and only process files that are requested by users or participants in the data space. To facilitate this, we have created a REST API to handle the process. Once it receives a user's request for predictions, the API processes the raw files and converts them to the [Smart Data Model Weather Forecast Series](../../SmartDataModels/WeatherForecastSeries.md) format, thus providing standardised predictions for ease of use.

### Components of the data flow

The components of the data flow used to collect predictions are as follows:

- **[Airflow](https://airflow.apache.org/):** Como se explica en el [flujo de datos de tiempo real](../real_time_data_flow/index.md) Airflow is responsible for orchestrating and scheduling the periodic acquisition of prediction data. It is the only component shared between both data flows.

- **[Bucket S3](https://apuntes.de/aws-certificacion-csaa/buckets/#gsc.tab=0):** Used to store raw prediction files obtained from Open-Meteo. These files contain forecasts for different models, variables and time horizons and are kept unprocessed until requested.

- **SmartFlow API:** REST API designed to manage access to prediction data. It retrieves raw files from the S3 bucket, processes them on demand and transforms the data into Smart Data Models, ensuring consistency and interoperability across the data space.

- **[APISIX](https://apisix.apache.org/):** An API Gateway that acts as the single entry point to the data space services. It is responsible for handling authentication, authorization and request routing, ensuring that only authorized users or services can access internal components. This component is already in the Fiware Data Space Connector.

### Stages of data flow

As explained above, the prediction data flow follows a demand-driven lifecycle that optimises storage and processing resources:

- **Data acquisition:** Prediction data from multiple climate models is periodically retrieved through Open-Meteo or using Airflow and stored as raw files in the S3 bucket.

- **On-demand processing:** When a user or service requests prediction data, the SmartFlow API identifies and loads the relevant raw files from S3.

- **Standardisation:** The requested data is transformed into the Weather Forecast Series Smart Data Model, converting variables, units and structures into a common representation.

- **Delivery:** The standardised prediction data is returned to the requester through the API, ready for direct use in simulations, dashboards or decision-support tools.

To visually understand the data flow, a flow chart has been created that captures the passage of data between the different components of the flow and the interactions between them.

![Predictions data flow image](../images/predictions_flow.png){ width="1200" }

As shown in the diagram, access to prediction data is always mediated by the SmartFlow API, which acts as the entry point to the raw prediction files stored in Amazon S3 and ensures that all outputs conform to the Smart Data Models used within the PGTEC data space. 

All user and service requests are first routed through APISIX, which acts as the API Gateway and security entry point of the FIWARE connector. APISIX is responsible for authentication and authorization, ensuring that only authenticated dashboards or services can access the available endpoints. Once the credentials are validated, APISIX routes each request to the appropriate internal service, in this case, the SmartFlow API.

This architecture enforces a single, secure entry point to the prediction services while maintaining a clear separation between access control, routing and data processing within the PGTEC data space.

