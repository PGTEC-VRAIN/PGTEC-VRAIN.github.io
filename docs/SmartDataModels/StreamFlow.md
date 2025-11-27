
This section presents a proposal for the creation of a new **Smart Data Model** designed to represent **hydrological information** from the *Confederación Hidrográfica del Júcar (CHJ)*.  
The objective is to standardize the collection, integration, and exchange of **river discharge and reservoir data** within the **PGTEC project** framework. Specifically, data from three different types of hydrological data will be stored:

- [Eiver discharge data](https://saih.chj.es/mapa-aforos)
- [Precipitation data](https://saih.chj.es/mapa-lluvias)
- [Reservoirs data](https://saih.chj.es/mapa-embalses)

Consequently, the proposed Smart Data Model will serve to standardize diverse climatic data, all sourced from the CHJ.
---

### Purpose

The **StreamFlow** model aims to provide a unified structure to represent real-time and historical hydrological variables obtained from CHJ monitoring stations.  
By aligning with the **FIWARE Smart Data Models** ontology, this new model ensures **semantic interoperability** with other environmental and meteorological datasets used in the project.

---

### Main Variables of Interest

| Parameter | Description | Unit |
|:-----------|:-------------|:------:|
| **Inflow** | Volume of incoming river water | m³/s |
| **Outflow** | Volume of outgoing river water | m³/s |
| **Water Level** | Elevation of the river or reservoir surface | m |
| **Volume** | Total stored water in the reservoir | m³ |
| **Filling Percentage** | Calculated percentage of capacity (0.0 to 1.0) |	% |	
| **Water Flow** | Rate of water discharge at a specific point | m³/s |	
| **Stream Flow** | Flow rate of the specific stream/tributary | m³/s |	
| **Sediment Flow**	| Rate of sediment transport in the water | kg/s |
| **Precipitation**	| Amount of water in 1 hour| mm/s |

These variables are critical for hydrological modeling, water resource management, and integration with simulation tools such as **TETIS**. These data will be used for getting the initial conditions of the basins of interest. These initial conditions are part of the TETIS input data. The rest of the data needed to train the TETIS model are the predictions that will come from another data sources such as Open-Meteo. To understand better the predictions environment created to extract different forecasts from a lot of climate models check the [SmartFlow Environment](https://pgtec-vrain.github.io/SmartFlow/).

---

### Model Definition

The proposed **StreamFlow** entity introduces the necessary attributes and metadata fields to harmonize **CHJ hydrological data** with the FIWARE ecosystem.  
It supports contextual information management through the **Orion Context Broker**, enabling real-time ingestion and storage into the **TimeScaleDB** which is a Postgres database designed for time series data that enables the historization of real time data for future uses such as dashboards or training new climate models. For more information about the real time data pipeline go to the [DataFlow section](https://pgtec-vrain.github.io/pipeline/).

---

### Repository

The model implementation in python can be found in the following Github repository:

> 🔗 [**GitHub – StreamFlow Model Definition**](https://github.com/PGTEC-VRAIN/WorkflowPTGEC/blob/juan/tetis/hydrographic_models.py)

---

