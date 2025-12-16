## PGTEC Data Space Arquitecture

This section describes the technical architecture of the PGTEC data space: 

- How participants connect?
- Ehich common services are provided?
- How FIWARE components are used to guarantee interoperability, security and governance?

It complements the high-level introduction given in the main [Data Space](index.md) page.

The architecture is designed to:

- Enable multiple organisations to share climate and hydrological data and services
- Keep each participant in control of the data they expose
- Apply common rules for trust, access control and interoperability

At the centre of this architecture are FIWARE Data Space Connectors (FDSC) and a set of shared trust services deployed in a cloud-native environment.

### Participants and Roles

From the perspective of the data space, the main participants are grouped into roles.

- **Data Providers**  
  Organisations that expose observed or forecast data through their own connector.  
  Examples: AEMET, CHJ, SIAR, AVAMET, Copernicus and other climate data providers.

- **Service Providers**  
  Organisations that expose value-added services (hydrological models, dashboards, simulations) that consume data from the space and publish results back as services.  
  Examples: IIAMA, VRAIN.

- **Data Consumers**  
  Any participant that queries the data space to consume datasets or services published by providers.

Most real participants play more than one role. For example, IIAMA and VRAIN consume climate data and provide services based on that information. 

### High-level architecture

At a high level, the PGTEC data space is composed of:

1. A set of FIWARE Data Space Connectors, one per participating organisation
2. Common trust and governance services: Trust Anchor, Verifiable Credentials Issuer and Marketplace
3. A cloud-native infrastructure that hosts these components on Kubernetes in AWS

Each participant connects to the data space through *its own* FIWARE Data Space Connector. The connector acts as a standardised gateway where:

- Incoming requests are authenticated and authorised
- Usage policies are enforced
- Data is exposed through interoperable APIs based on NGSI-LD and TM Forum standards

Shared components such as the Trust Anchor and Marketplace provide ecosystem-wide services for identity, policy and discovery.

## Common trust and governance services

### Trust Anchor

The **Trust Anchor (TA)** is the main trust service in the PGTEC data space. It ensures that interactions and data exchanges happen only between authenticated, authorised and compliant participants. 

Its responsibilities include:

- Maintaining a **Trusted Issuers List** with the entities allowed to issue verifiable credentials within the ecosystem
- Providing endpoints that connectors can call to validate identities and credentials
- Acting as the root of trust that other components use when deciding whether to accept a connection

Technically, the TA runs as a microservice inside the Kubernetes cluster, backed by a relational database where trusted issuers and related trust configuration are stored. It is typically exposed via an ingress controller so that connectors can reach it over HTTPS from within the cloud or from other networks.

### Marketplace 

A **Marketplace** component is planned for later stages of the project. Its purpose is to:

- Allow providers to publish the data sets and services they offer
- Allow consumers to discover available resources
- Support negotiation of access conditions, prices or usage policies
- Integrate with contract management mechanisms from the FDSC

For the first **Minimum Viable Data** Space the full Marketplace is not strictly required, because each connector already exposes TM Forum APIs that allow programmatic discovery of catalogues and offers. This keeps the initial deployment simpler while preserving the core functionality.

### Verifiable Credentials Issuer 

The **Verifiable Credentials (VC) Issuer** is another planned shared service. 

- Issue verifiable credentials to organisations, services and possibly users
- Integrate with the Trust Anchor and its Trusted Issuers List
- Provide the credentials that connectors use when authenticating incoming requests

In early stages of the project, identities and access are managed with simpler mechanisms. As the data space opens to more external participants, the VC Issuer becomes crucial to support self-sovereign identities and more advanced trust models.

## FIWARE Data Space Connector

The FIWARE Data Space Connector (FDSC) is the main technical building block of the PGTEC data space. Each provider or consumer uses its own connector instance to interface with the rest of the ecosystem. 

Conceptually, the FDSC provides:

- Authentication and authorisation based on verifiable credentials and policies
- Data publication and discovery through standard APIs
- Contract and policy management for data usage
- Actual data exchange between connectors using the Dataspace protocol

Internally, the FDSC is itself composed of several subsystems, which can be grouped by function: 

### Authentication and authorisation

- **Policy Decision Point (PDP) plugin**  
  Evaluates access policies written in Open Digital Rights Language (ODRL) and decides whether a request should be allowed.

- **APISIX API Gateway**  
  Terminates incoming HTTP(S) traffic, enforces the PDP decisions and routes authorised requests to internal services such as brokers or APIs.

- **VC Verifier**  
  Checks the validity of verifiable credentials presented by participants.

- **Trusted Issuer List and Credentials Config Service**  
  Maintain the configuration and state related to trusted issuers and stored credentials.

### Data publication and discovery

- **Scorpio NGSI-LD Broker**  
  Manages publication, query and subscription of context data. This is where harmonised entities (for example, observations or forecasts) are stored and exposed using NGSI-LD.

- **TM Forum APIs and Contract Management**  
  Allow providers to publish catalogues and assets, and to define and manage usage contracts between participants.

### Dataspace protocol and dataplane

- **Rainbow (IDSA Dataspace Protocol implementation)**  
  Implements the International Data Spaces Association protocol for secure data exchange between connectors.

- **Trusted Policy Propagator (TPP)**  
  Distributes policies between participants to ensure that usage constraints are consistently enforced.

- **DID and dataplane services**  
  Manage decentralised identifiers and the actual data transfer channel, ensuring that policies and security rules are applied during data movement.

This modular design allows each connector to be extended with additional components when needed. For example, climate data providers add components such as Orion-LD, TimescaleDB, Mintaka, Airflow or SmartFlow API to handle their specific data ingestion and exposure needs. :contentReference[oaicite:9]{index=9}

## Minimum Viable Data Space (MVDS)

Before deploying the full architecture, PGTEC defines a Minimum Viable Data Space (MVDS) that focuses on validating the interaction between key components and participants.

The MVDS includes:

- **Trust Anchor**
- **Connectors** for a subset of data providers (climate agencies)
- A **connector** for **IIAMA**, acting as consumer of climate data and provider of hydrological services

In this first deployment:

- The Marketplace is not deployed, since all necessary discovery can be performed through the TM Forum APIs already available in each connector.
- The Verifiable Credentials Issuer is not yet required, because only internal PGTEC participants are involved.
- The connector for VRAIN can be added later, once the real-time dashboard service is ready to be integrated.

Even in this reduced configuration, the MVDS provides a functional dataspace where realistic scenarios can be simulated and the behaviour of connectors, models and services can be evaluated.

## Infrastructure and Deployment

The PGTEC data space is deployed on a public cloud infrastructure, specifically on AWS, using a Kubernetes cluster as the underlying orchestration platform.

The main reasons for this choice are:

- **Scalability**  
  The cluster can be scaled up or down depending on the computational and storage needs (for example, when ingesting large climate datasets or running intensive simulations).

- **Resilience**  
  Distributed services with built-in redundancy ensure operational continuity, even in the presence of failures.

- **Security**  
  Integration with cloud identity and access management, network segmentation and encryption aligns with European digital trust standards.

- **Flexibility**  
  Native support for containers and microservices simplifies the deployment of connectors, Trust Anchor, and additional components such as Orion-LD, Mintaka, TimescaleDB, Airflow or SmartFlow.

Within this cluster, each connector runs in its own namespace, along with its auxiliary services. This separation allows providers to manage their own components, while still benefiting from a shared, managed infrastructure.

## Relation with other documentation

This architecture page connects to the rest of the technical documentation as follows:

- The [Data Sources](../data_sources/index.md) and [Data and services](../getting_started/data_and_services.md) pages describe which datasets and services are actually exposed through the connectors.
- The [Data Flow](../pipeline/index.md) and [SmartFlow](../SmartFlow/index.md) pages detail how observed and forecast data are ingested, harmonised, stored and exposed.
- The [Identities and verifiable credentials](identities_and_credentials.md) page explains the identity and trust layer that runs on top of this architecture.
- The [DIDs](did.md) page shows how decentralised identifiers are generated and used to support the identity layer in practice.