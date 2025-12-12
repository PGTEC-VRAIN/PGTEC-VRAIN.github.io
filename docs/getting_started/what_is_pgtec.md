# What is PGTEC?
## What is PGTEC?

PGTEC is a <strong>climate</strong> and <strong>weather</strong> data space that supports early warning and risk management for climate <strong>emergencies.</strong> It connects data providers, data users and digital services through shared standards, governance rules and interoperable components.

Instead of being a single data platform, PGTEC is designed as a shared space where multiple organisations can publish, access and reuse data under common technical standards and governance rules.

The project combines:

- Climate and weather predictions from several numerical models and providers.
- Hydrological and risk-related information used to feed early warning systems.
- An interoperable infrastructure based on FIWARE technologies, Smart Data Models and Data Space components.

### Why a data space and not just a data platform?

Traditional data platforms usually belong to a single organisation and expose their own APIs and formats. A data space introduces additional concepts:

- Shared governance instead of a single owner.
- Common data models and APIs to reduce integration costs.
- Trust and identity mechanisms to control who can access what.
- The possibility to connect multiple platforms rather than replacing them.

In the European context, data spaces are promoted as a way to enable secure and sovereign data sharing between organisations, particularly in domains such as smart cities, mobility and climate services.

PGTEC applies these ideas to the specific domain of climate emergency management.

## PGTEC high-level architecture

At a very high level, PGTEC can be seen as four layers:

1. <strong>Data Sources</strong>  
   Climate and hydrological data are periodically retrieved from several providers such as AEMET, Confederación Hidrográfica del Júcar, Open-Meteo and Copernicus services.

2. <strong>Data ingestion and processing </strong>  
   The SmartFlow component orchestrates Python scripts and Airflow workflows that download forecasts, transform them using Smart Data Models and prepare them for storage and service exposure.

3. <strong>Context management and storage</strong>  
   Harmonised entities are stored in a FIWARE Context Broker with historical persistence, enabling both real-time queries and time-series analysis for machine learning and hydrological models.

4. <strong>Services and Applications</strong>  
   FastAPI services expose processed data through RESTful APIs and feed dashboards, such as the one used to configure inputs for the TETIS hydrological model.

## Technologies

PGTEC relies on several key technologies that appear across the documentation:

- <strong>FIWARE Context Broker</strong>    
  Manages context information and exposes NGSI-LD APIs, acting as the core registry of entities in the data space.

- <strong>Smart Data Models</strong>    
  Provide a common schema for climate variables, hydrological indicators and risk entities so that data from different sources can be compared and combined consistently.

- <strong>SmartFlow</strong>    
  A collection of Airflow DAGs and FastAPI services, with Docker-based deployment, that automates data retrieval, transformation and publication. 

- <strong>Decentralized Identifiers (DIDs)  </strong>  
  Used to uniquely identify organisations, services or components in a self-sovereign way, without relying on a single central authority. PGTEC demonstrates the use of did:web and did:key methods together with Docker-based tooling to generate DID documents.

!!! Tip "More details"

    If you want to dive into the technical details after this overview:

    - See [Data Flow](../pipeline/index.md) for an end-to-end description of the ingestion pipeline.
    - See [Smart Data Models](../SmartDataModels/index.md) for the entity schemas used across the project.
    - See [SmartFlow](../SmartFlow/index.md) if you are planning to run the pipelines or services locally.
    - See [Data Space](../DataSpace/index.md) for the architecture, governance and trust model of the PGTEC data space.