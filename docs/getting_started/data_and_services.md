# Data and Services
## Data and Services in PGTEC
This page answers the question:

<strong> What does PGTEC offer in practice?</strong>

PGTEC brings together climate, hydrological and risk-related information, processes it through a common pipeline and exposes it as interoperable services that can be reused by different applications.

## Data Sources

The detailed description of each source is available in the [Data Sources](../data_sources/index.md) section. Here we summarise the main categories:

- <strong>Numerical weather prediction models</strong>    
  Forecasts from several models are retrieved programmatically, including configurations such as HARMONIE/AROME, ARPEGE, ICON, AIFS and GFS.

- <strong>Hydrological and flood-related services</strong>   
  Products from Copernicus services such as EFAS or EFFIS are integrated when relevant for early flood or fire risk assessment.

- <strong>National and regional agencies</strong>   
  Data from organisations such as AEMET and the Confederación Hidrográfica del Júcar contributes local accuracy and observations needed to validate or complement modelled information.

Each source is mapped to one or more Smart Data Models so that variables like temperature, precipitation or discharge share the same structure regardless of the original provider.

### From raw data to context entities

The transformation from raw files or external APIs into PGTEC entities follows these steps:

1. <strong>Retrieval</strong>   
   Airflow DAGs periodically call the external APIs or download files from each data provider.

2. <strong>Transformation</strong>   
   Python scripts convert the raw input into entities that follow Smart Data Models. This includes handling coordinates, time grids, units and metadata.

3. <strong>Loading into the Context Broker</strong>   
   The transformed entities are pushed into a FIWARE Context Broker, where they can be queried using a common NGSI-LD interface.

4. <strong>Historical storage</strong>   
   Historical extensions keep track of time series so that models and dashboards can access both the latest situation and past evolution.

All these steps are orchestrated by the [SmartFlow](../SmartFlow/index.md) component, which provides Docker-based deployment, Airflow configuration and FastAPI services.

## Services 

Once data is harmonised and stored in the Context Broker, PGTEC enables several types of services:

- <strong>Data-as-a-Service APIs</strong>    
  FastAPI endpoints expose subsets of data tailored to specific use cases, for example climate predictions for a given point of interest or catchment. These services can be called from external applications or dashboards. 

- <strong>Support for hydrological modelling</strong>    
  The PGTEC pipeline feeds the configuration of the TETIS hydrological model, allowing users to select sources and locations from a dashboard, which then triggers the underlying FastAPI logic.

- <strong>Early warning and risk indicators</strong>    
  By combining meteorological and hydrological information, PGTEC can compute derived indicators for flood or drought risk that support early warning workflows.

- <strong>Experimentation and research</strong>    
  Since data is exposed in a standardised way, it can be reused for machine learning, downscaling or impact modelling without having to reimplement the ingestion logic for each project.

!!! Tip "More details"

    If you are mainly interested in the content that PGTEC provides:

    - Start with [Data Sources](../data_sources/index.md) to see each provider and variable in detail.
    - Continue with [Smart Data Models](../SmartDataModels/index.md) to understand how entities are structured.
    - If you want to run the pipelines or services yourself, go to [SmartFlow](../SmartFlow/index.md), which explains cloning the repository and starting Docker containers.
