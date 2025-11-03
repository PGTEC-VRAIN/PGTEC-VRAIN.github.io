
This section presents a proposal for the creation of a new **Smart Data Model** designed to represent **hydrological information** from the *Confederación Hidrográfica del Júcar (CHJ)*.  
The objective is to standardize the collection, integration, and exchange of **river discharge and reservoir data** within the **PGTEC project** framework.

---

### 🌊 Purpose

The **StreamFlow** model aims to provide a unified structure to represent real-time and historical hydrological variables obtained from CHJ monitoring stations.  
By aligning with the **FIWARE Smart Data Models** ontology, this new model ensures **semantic interoperability** with other environmental and meteorological datasets used in the project.

---

### 📏 Main Variables of Interest

| Parameter | Description | Unit |
|:-----------|:-------------|:------:|
| **Inflow** | Volume of incoming river water | m³/s |
| **Outflow** | Volume of outgoing river water | m³/s |
| **Water Level (Height)** | Elevation of the river or reservoir surface | m |
| **Volume** | Total stored water in the reservoir | m³ |

These parameters are critical for hydrological modeling, water resource management, and integration with simulation tools such as **TETIS**.

---

### 🧩 Model Definition

The proposed **StreamFlow** entity introduces the necessary attributes and metadata fields to harmonize **CHJ hydrological data** with the FIWARE ecosystem.  
It supports contextual information management through the **Orion Context Broker**, enabling real-time ingestion, storage, and querying of flow observations.

---

### 📚 Repository

The model implementation and schema definition can be found in the following repository:

> 🔗 [**GitHub – StreamFlow Model Definition**](https://github.com/PGTEC-VRAIN/WorkflowPTGEC/blob/juan/tetis/hydrographic_models.py)

---

> 💡 *The StreamFlow Smart Data Model complements the existing WeatherObserved and WeatherForecastSeries models, forming a complete data representation framework for meteorological and hydrological information within PGTEC.*


