# What do I need?

To correctly deploy and operate the data pipeline, the following components and requirements must be available:

- **Python:** Required for implementing auxiliary scripts, data preprocessing tasks, and integration logic with external services.

- **Docker Compose:** Used to orchestrate and deploy the FIWARE stack.

- **Airflow:** Provides workflow orchestration, ensuring the automated and scheduled execution of data collection, transformation, and loading tasks.

- **Access credentials**: An API key or endpoint URL to connect to the external data sources supplying the raw information.

- **Networking and FIWARE configuration:** Proper network setup and FIWARE component configuration to allow seamless communication between all services in the stack.