# Set up environment

This [repository](https://github.com/PGTEC-VRAIN/Entorno-AirFlow_IotAgent_OrionLD_QuantumLeap) provides a complete environment for orchestration and management of IoT data, integrating a set of FIWARE-based components and workflow automation tools.

##   Core Components

- **IoT Agent:** Interface for receiving IoT device data and forwarding it to the appropriate FIWARE context entities.
- **Orion-LD Context Broker:** Core NGSI-LD–based context management engine responsible for storing, updating, and distributing contextual information.
- **QuantumLeap:** Time-series database service that persists historical events and temporal data, supporting advanced analytics and AI model training.
- **CrateDB:** Serves as the historical storage backend within the FIWARE stack.
- **MongoDB:** Provides context data persistence for the Orion-LD Context Broker.
- **Apache Airflow:** Workflow orchestration through Directed Acyclic Graphs (DAGs), enabling automation and scheduling of data-processing pipelines.

## Repository Contents

- **docker-compose.yml**: Defines and configures all services and containers within the stack.

- **dags/**: Directory containing Airflow DAGs for automated workflows.

- **Scripts:**
    - **AEMET.py:** Fetches meteorological data from the AEMET API.
    - **Copernicus.py:** Retrieves Copernicus climate datasets for the province of Valencia using Python’s cdsapi library.
    - **Flujo_Copernicus_orion.py:** DAG that collects Copernicus data, registers it in the IoT Agent, and stores it in Orion-LD.
    - **Flujo_copernicus_orion_quantumleap.py:** Enhanced DAG that extends the previous workflow by integrating QuantumLeap for historical data persistence in CrateDB. (Recommended DAG for production use.)

##  **Setup instructions**

### **Clone the repository**
```
git clone https://github.com/PGTEC-VRAIN/Entorno-AirFlow_IotAgent_OrionLD_QuantumLeap.git
cd Entorno-AirFlow_IotAgent_OrionLD_QuantumLeap
```
### **Start the containers**
```
docker-compose up -d --build
```

- Use --build only if changes were made to the docker-compose.yml.

- The -d option runs services in the background (detached mode).
### **Verify running services**
```
docker ps
```
### **Shut down the environment**

- From a new terminal:
```
docker-compose down
```
- Or interrupt the current process with CTRL + C.