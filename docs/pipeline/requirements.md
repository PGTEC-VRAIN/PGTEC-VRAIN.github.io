## What do I need?

To correctly deploy and operate the data pipeline, the following components and requirements must be available:

- **Python:** Required for implementing auxiliary scripts, data preprocessing tasks, and integration logic with external services.

- **Docker Compose:** Used to orchestrate and deploy the FIWARE stack.

- **Airflow:** Provides workflow orchestration, ensuring the automated and scheduled execution of data collection, transformation, and loading tasks.

- **Access credentials**: An API key or endpoint URL to connect to the external data sources supplying the raw information.

- **Networking and FIWARE configuration:** Proper network setup and FIWARE component configuration to allow seamless communication between all services in the stack.

##   Core Components

- **IoT Agent:** Interface for receiving IoT device data and forwarding it to the appropriate FIWARE context entities.
- **Orion-LD Context Broker:** Core NGSI-LD–based context management engine responsible for storing, updating, and distributing contextual information.
- **QuantumLeap:** Time-series database service that persists historical events and temporal data, supporting advanced analytics and AI model training.
- **CreateDB:** Serves as the historical storage backend within the FIWARE stack.
- **MongoDB:** Provides context data persistence for the Orion-LD Context Broker.
- **Apache Airflow:** Workflow orchestration through Directed Acyclic Graphs (DAGs), enabling automation and scheduling of data-processing pipelines.

This project was developed and tested on: 

- **Ubuntu 24.04.1 LTS**

These are the necessary requirements to be able to execute the project:


| Software | Version / Note
|:-------|:-------
|[Docker](https://docs.docker.com/engine/install/ubuntu/)| 27.2.0 
|[Docker Compose](https://docs.docker.com/compose/install/)| 27.2.0 
|[Python](https://www.python.org/)| Docker container
|[Airflow](https://airflow.apache.org/)| Docker container 
|[IoT Agent-UL](https://fiware-tutorials.readthedocs.io/en/latest/iot-agent.html)| Docker container
|[Orion-LD Context Broker](https://fiware-orion.readthedocs.io/en/master/)| Docker container
|[QuantumLeap](https://quantumleap.readthedocs.io/en/latest/)| Docker container / CreateDB backend
